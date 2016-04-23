---
layout: post
title: Handy HELIO SQL queries
date: 2016-04-23
time: "13:40:00"
blog: "true"
categories: ["Space Weather", "community"]
---

This is a number of queries that I've come up with over the years to obtain
different results using [HELIO](http://helio-vo.eu) services. I hope these
examples help you to build the queries you need to solve your science questions.
I will update this post as I find new fancy ways to use this system.

# [HELIO Event Catalogue (HEC)](http://hec.helio-vo.eu/)

The HEC provides a number of catalogues about events in the heliosphere, some of
them have been built automatically while others were manually gathered. Check
each catalogue source for the information about what it contains and how has
been populated.

## [Group flares per month and type](http://hec.helio-vo.eu/hec/hec_gui_free.php?sql=SELECT+DATE_TRUNC%28%27month%27%2C+time_start%29+AS+month%2C++SUBSTRING%28xray_class+from+1+for+3%29+AS+xray%2C+COUNT%28*%29+FROM+goes_sxr_flare+WHERE+time_start+%3E+%272002-01-01%27+GROUP+BY+month%2Cxray+ORDER+BY+month%0D%0A)

{% highlight sql %}
SELECT 
    DATE_TRUNC('month', time_start) AS month, SUBSTRING(xray_class from 1 for 3) AS xray, 
    COUNT(*) 
  FROM goes_sxr_flare 
    WHERE time_start > '2002-01-01' 
    GROUP BY month,xray 
    ORDER BY month
{% endhighlight %}

## [ascii histogram](http://hec.helio-vo.eu/hec/hec_gui_free.php?sql=SELECT++EXTRACT%28year+from+time_start%29+AS+year%2C+COUNT%28*%29+as+count%2C+REPEAT%28%27*%27%2C%28%28COUNT%28*%29%29%3A%3AINT%29%29+AS+bar+FROM+goes_sxr_flare+WHERE+time_end+%3E%3D+%28time_start+%2B+INTERVAL+%272+hours%27%29++GROUP+BY+year+ORDER+BY+year%0D%0A)

{% highlight sql %}
SELECT 
    EXTRACT(year from time_start) AS year, COUNT(*) as count, 
    REPEAT('*',((COUNT(*))::INT)) AS bar 
  FROM goes_sxr_flare 
    WHERE time_end >= (time_start + INTERVAL '2 hours')  
    GROUP BY year ORDER BY year
{% endhighlight %}

## [Number of Flares per year longer than two hours](http://hec.helio-vo.eu/hec/hec_gui_free.php?sql=select++extract%28year+from+time_start%29+as+year%2C+count%28*%29+as+count%2C+repeat%28%27*%27%2C%28%28count%28*%29%29%3A%3Aint%29%29+as+bar+from+goes_sxr_flare+where+time_end+%3E%3D+%28time_start+%2B+interval+%272+hours%27%29++group+by+year+order+by+year%0D%0A)

{% highlight sql %}
SELECT 
    EXTRACT(year from time_start) AS year, COUNT(*) as count, 
    REPEAT('*',((COUNT(*))::INT)) AS bar 
  FROM goes_sxr_flare 
    WHERE time_end >= (time_start + INTERVAL '2 hours') 
    GROUP BY year
    ORDER BY year
{% endhighlight %}

## [Long duration flares happening in the north hemisphere and close to the central meridian](http://hec.helio-vo.eu/hec/hec_gui_free.php?sql=select+*+from+goes_sxr_flare+where+time_end+%3E%3D+time_start+%2B+interval+%272+hours%27+and+%28long_hg+between+-5.0+and+5.0%29+and+lat_hg+%3E%3D+0+order+by+time_start%0D%0A)

{% highlight sql %}
SELECT * FROM goes_sxr_flare
    WHERE time_end >= time_start + interval '2 hours' AND
          (long_hg BETWEEN -5.0 AND 5.0) AND
          lat_hg >= 0 
    ORDER BY time_start
{% endhighlight %}

## [Hours from a date and other operations in other fields](http://hec.helio-vo.eu/hec/hec_gui_free.php?sql=select+extract+%28EPOCH+from+time_start+-+date+%272003-01-01%27%29%3A%3Aint%2F3600.+as+hours%2C+duration%2C+pa%2C+pa_width%2C+pa+-+pa_width%2F2+as+pa_neg%2C+pa+%2B+pa_width%2F2+as+pa_pos%2C+v+from+cactus_soho_cme+where+time_start+between+%272003-01-01%27+and+%272004-01-01%27%0D%0A%0D%0A%0D%0A)

{% highlight sql %}
SELECT EXTRACT(EPOCH from time_start - date '2003-01-01')::int/3600. as hours, 
       duration, pa, pa_width, pa - pa_width/2 as pa_neg, pa + pa_width/2 as pa_pos, v 
   FROM cactus_soho_cme 
     WHERE time_start BETWEEN '2003-01-01' AND '2004-01-01'
{% endhighlight %}

## [Time of ARs between anything and beta-gamma-delta](http://hec.helio-vo.eu/hec/hec_gui_free.php?sql=select+bgd.nar%2C+extract%28%27days%27+from+%28bgd.mint-nbgd.maxt%29%29+as+dift%2C+bgd.bgd_n%2C+nbgd.maxt%2C+bgd.mint%2C+nbgd.mag_class+from+%28select+nar%2C+min%28time_start%29+as+mint%2C+count%28*%29+as+bgd_n+from+noaa_active_region_summary+where+time_start%3E%3D%272012-03-01+00%3A00%3A00%27+AND+time_start%3C%3D%272016-04-01+23%3A59%3A59%27+and+mag_class%3D%27Beta-Gamma-Delta%27+group+by+nar%29+bgd+inner+join+%28select+nar%2C+max%28time_start%29+as+maxt%2C+mag_class+from+noaa_active_region_summary+where+time_start%3E%3D%272012-03-01+00%3A00%3A00%27+AND+time_start%3C%3D%272016-04-01+23%3A59%3A59%27+and+mag_class!%3D%27Beta-Gamma-Delta%27+group+by+nar%2C+mag_class+order+by+nar%29+nbgd+on+%28bgd.nar+%3D+nbgd.nar%29+where+bgd.mint+%3E+nbgd.maxt)

{% highlight sql %}
SELECT
   bgd.nar, EXTRACT('days' from (bgd.mint-nbgd.maxt)) as dift, bgd.bgd_n, 
   nbgd.maxt, bgd.mint, nbgd.mag_class 
FROM 
   (
   SELECT 
      nar, MIN(time_start) as mint, COUNT(*) as bgd_n 
     FROM noaa_active_region_summary 
       WHERE time_start>='2012-03-01 00:00:00' AND time_start<='2016-04-01 23:59:59' AND 
             mag_class='Beta-Gamma-Delta' 
       GROUP BY nar
   ) bgd 
INNER JOIN 
   (
   SELECT 
      nar, MAX(time_start) as maxt, mag_class 
   FROM noaa_active_region_summary 
     WHERE time_start>='2012-03-01 00:00:00' AND time_start<='2016-04-01 23:59:59' AND 
           mag_class!='Beta-Gamma-Delta' 
     GROUP BY nar, mag_class 
     ORDER BY nar
   ) nbgd 
ON (bgd.nar = nbgd.nar) WHERE bgd.mint > nbgd.maxt
{% endhighlight %}

## [Join GOES and RHESSI events around the 2003 Halloween event](http://hec.helio-vo.eu/hec/hec_gui_free.php?sql=select+g.time_start+as+GOES_Ts%2C+r.time_start+as+RHESSI_Ts%2C+g.xray_class%2C+%28g.time_start+-+r.time_start%29+as+Dt+from+goes_sxr_flare+g%2C+rhessi_hxr_flare+r+where+g.time_start+between+%272003-10-20%27+and+%272003-11-10%27+and+%28g.time_start%2C+g.time_end%29+overlaps+%28r.time_start%2C+r.time_end%29+and+g.time_end+%3E%3D+g.time_start+%2B+interval+%272+hours%27%0D%0A)

{% highlight sql %}
SELECT g.time_start as GOES_Ts, r.time_start as RHESSI_Ts, 
       g.xray_class, (g.time_start - r.time_start) as Dt
  FROM goes_sxr_flare g, rhessi_hxr_flare r
    WHERE g.time_start BETWEEN '2003-10-20' AND '2003-11-10' AND
          (g.time_start, g.time_end) OVERLAPS (r.time_start, r.time_end) AND
          g.time_end >= g.time_start + INTERVAL '2 hours'
{% endhighlight %}

## [CMEs after flares from an Active Region](http://hec.helio-vo.eu/hec/hec_gui_free.php?sql=select+goes.time_start+as+goes_ts%2C+goes.nar%2C+goes.lat_hg%2C+goes.xray_class%2C+cme.time_start+as+cme_ts%2C+cme.pa_width%2C+cme.event_detail+from+goes_sxr_flare+as+goes%2C+cactus_soho_cme+as+cme+where+cme.time_start+between+%28goes.time_start+%2B+interval+%2730+minutes%27%29+and+%28goes.time_start+%2B+interval+%274+hours%27%29+and+goes.nar+%3D+11389+and+goes.xray_class+%3E+%27C%27+order+by+goes.time_start%2C+cme.pa_width%0D%0A)

{% highlight sql %}
SELECT goes.time_start as goes_ts, goes.nar, goes.lat_hg, goes.xray_class, 
       cme.time_start as cme_ts, cme.pa_width, cme.event_detail
  FROM goes_sxr_flare AS goes, cactus_soho_cme AS cme 
    WHERE cme.time_start BETWEEN (goes.time_start + INTERVAL '30 minutes') AND 
                                 (goes.time_start + INTERVAL '4 hours') AND
          goes.nar = 11389 AND
          goes.xray_class > 'C'
    ORDER BY goes.time_start, cme.pa_width
{% endhighlight %}

# [HELIO Feature Catalogue (HFC)](http://hfc.helio-vo.eu)

The HFC provides access to features detected by codes running within HELIO
systems, that includes active regions, sunspots, coronal holes, etc. Some of
these features have been detected by different codes - check the information of
each algorithm to understand their limitations. To use the
[SQL query](http://voparis-helio.obspm.fr/hfc-gui/hfc_sql_query.php) you have
first to remove the line breaks in the queries below.

## Number of filaments seen per month when ARs detected by SMART were present

{% highlight sql %}
SELECT EXTRACT(year from fil.date_obs) AS year, 
       EXTRACT(month from fil.date_obs) AS month, COUNT(1) 
   FROM view_fil_hqi AS fil, view_ar_hqi AS ar
     WHERE fil.date_obs BETWEEN '1997-03-25' AND '1998-06-16' AND
           ar.date_obs BETWEEN '1997-03-25' AND '1998-06-16' AND 
           DATE(fil.date_obs)=DATE(ar.date_obs) AND 
           ar.noaa_number IS NOT NULL AND 
           ar.code="SMART" 
     GROUP BY year, month
     ORDER BY year, month
{% endhighlight %}


# [Instrument Location Service (ILS)](http://helio-vo.eu/services/interfaces/helio-ils_uix.php)

The ILS provides information about the location of planets and some spacecraft
in the heliosphere. This is very useful to find, for example when STEREO A was
at certain degrees away from Earth or other spacecraft.

## [One value per month per orbit](http://helio-vo.eu/services/interfaces/helio-ils_soap8.php?qtype=0&sql=SELECT+MONTH%28time%29+AS+month%2C+time%2C+target_obj%2Cdate%28time%29+as+time+from+trajectories+where+time+between+%272002-10-28%27+and+%272003-11-03%27+AND+%28target_obj%3D%27Earth%27%29+GROUP+BY+MONTH%28Time%29&format=html&process=1)

*Don't remember what I was trying to do with this*

{% highlight sql %}
SELECT MONTH(time) AS month, time, target_obj,date(time) as time 
  FROM trajectories 
    WHERE time BETWEEN '2002-10-28' AND '2003-11-03' AND 
          target_obj='Earth'
    GROUP BY MONTH(Time)
{% endhighlight %}

