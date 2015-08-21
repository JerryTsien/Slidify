---
title       : Visualized World Economy
subtitle    : Based on the IMF World Economic Outlook Database
author      : Jerry Tsien
job         : Data Scientist
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [nvd3]            # {mathjax, quiz, bootstrap}
ext_widgets : {rCharts: libraries/nvd3}
mode        : selfcontained   # {standalone, selfcontained, draft}
knit        : slidify::knit2slides
---



## Exciting Features  

1. Interactive world and continental map  
2. Animated chart of three types: bars, line, and scatter points  
3. Flexible data table, fully sortable and searchable  

## Included Economic Indicators  

1. Real GDP growth  
2. Inflation  
3. Budget balance / GDP  
4. Current account balance / GDP  

# for 189 countries in 36 years (1980-2015)  

--- .class #id 

## Chart Preview  


<div id = 'Preview' class = 'rChart nvd3'></div>
<script type='text/javascript'>
 $(document).ready(function(){
      drawPreview()
    });
    function drawPreview(){  
      var opts = {
 "dom": "Preview",
"width":    800,
"height":    400,
"x": "Year",
"y": "US.Growth",
"type": "multiBarChart",
"id": "Preview" 
},
        data = [
 {
 "US.Growth":          2.666,
"Year": 2006 
},
{
 "US.Growth":          1.779,
"Year": 2007 
},
{
 "US.Growth":         -0.292,
"Year": 2008 
},
{
 "US.Growth":         -2.776,
"Year": 2009 
},
{
 "US.Growth":          2.532,
"Year": 2010 
},
{
 "US.Growth":          1.602,
"Year": 2011 
},
{
 "US.Growth":          2.321,
"Year": 2012 
},
{
 "US.Growth":          2.219,
"Year": 2013 
},
{
 "US.Growth":          2.389,
"Year": 2014 
},
{
 "US.Growth":          3.135,
"Year": 2015 
} 
]
  
      if(!(opts.type==="pieChart" || opts.type==="sparklinePlus" || opts.type==="bulletChart")) {
        var data = d3.nest()
          .key(function(d){
            //return opts.group === undefined ? 'main' : d[opts.group]
            //instead of main would think a better default is opts.x
            return opts.group === undefined ? opts.y : d[opts.group];
          })
          .entries(data);
      }
      
      if (opts.disabled != undefined){
        data.map(function(d, i){
          d.disabled = opts.disabled[i]
        })
      }
      
      nv.addGraph(function() {
        var chart = nv.models[opts.type]()
          .width(opts.width)
          .height(opts.height)
          
        if (opts.type != "bulletChart"){
          chart
            .x(function(d) { return d[opts.x] })
            .y(function(d) { return d[opts.y] })
        }
          
         
        
          
        

        
        
        
      
       d3.select("#" + opts.id)
        .append('svg')
        .datum(data)
        .transition().duration(500)
        .call(chart);

       nv.utils.windowResize(chart.update);
       return chart;
      });
    };
</script>

# Embedded R code showing economic growth in the US during 2006-2015.  

--- .class #id 

## Architecture

- Portable: Based on a subset of the IMF WEO Database (April 2015) for increased performance, but can be easily adapted to the full dataset  
- Reproducible: Developed with R, Shiny, GoogleVis, rCharts, and Slidify  
- Universal Access: accessible over the Internet  
- Open source and FREE  

--- .class #id 

## Resources  

# Visualized World Economy  
https://JerryTsien.shinyapps.io/vWorldEcon

Source code available at Github:  
https://github.com/JerryTsien/vWorldEcon

Original data from IMF:  
http://www.imf.org/external/pubs/ft/weo/2015/01/weodata/download.aspx

## Thank You!  
