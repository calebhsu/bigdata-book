# Warmup

Complete this warmup exercise to get an idea how to put all the different pieces
together to generate an end-to-end data analysis viz report.

<a name="top"/>
<div id="autonav"></div>

{% data src="../fcq/fcq.clean.json" %}
{% enddata %}

{% viz %}

{% title %}

What is the distribution of courses across colleges?

{% solution %}

var groups = _.groupBy(data, function(d){
    return d['CrsPBAColl']
})

var count = _.mapValues(groups, function(g) {
    return _.size(g)
})

var keys = _.keys(count)

var final = _.map(keys, function(key) {
    return {"name": key, "count": count[key]}
})

console.log(final)

function computeX(d, i) {
    return 40 * i
}

function computeHeight(d, i) {
    return d.count / 10
}

function computeWidth(d, i) {
    return 20
}

function computeY(d, i) {
    return 400 - (d.count / 10)
}

function computeColor(d, i) {
    return 'red'
}

function computeLabel(d, i) {
    return d.name.substring(0,2)
}

var viz = _.map(final, function(d, i){
    return {
        x: computeX(d, i),
        y: computeY(d, i),
        height: computeHeight(d, i),
        width: computeWidth(d, i),
        color: computeColor(d, i),
        label: computeLabel(d, i)
    }
 })
console.log(viz)

var result = _.map(viz, function(d){
         // invoke the compiled template function on each viz data
         return template({d: d})
     })
return result.join('\n')

{% template %}

<rect x="${d.x}"
      y="${d.y}"
      height="${d.height}"
      width="${d.width}"
      style="fill:${d.color};
             stroke-width:1;
             stroke:rgb(0,0,0)" />
<text x="${d.x}" y="${d.y - 10}">
    ${d.label}
</text>

{% endviz %}
