{% data src="fcq.clean.json" %}
{% enddata %}

# Warmup

Next, complete the following warmup exercises as a team.

## How many unique subject codes?

{% lodash %}
return _.uniq(_.pluck(data, 'Subject')).length
{% endlodash %}

They are {{ result }} unique subject codes.

## How many computer science (CSCI) courses?

{% lodash %}
return _.filter(data, function(d) {
    return (d.Subject === "CSCI")
}).length
{% endlodash %}

They are {{ result }} computer science courses.

## What is the distribution of the courses across subject codes?

{% lodash %}
var subjects = _.groupBy(data, 'Subject')

return _.mapValues(subjects, function(s) {
    return s.length
})

{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 100 courses?

{% lodash %}
var subjects = _.groupBy(data, 'Subject')
var ret = _.pick(_.mapValues(subjects, function(d) {
    return d.length
}), function(x){
    return x > 100
})
return ret
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 5000 total enrollments?

{% lodash %}
var subjects = _.groupBy(data, 'Subject')
var ret = _.pick(_.mapValues(subjects, function(d) {
    return _.sum(_.pluck(d, 'N.ENROLL'))
}), function(x){
    return x > 5000
})
return ret
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What are the course numbers of the courses Tom (PEI HSIU) Yeh taught?

{% lodash %}
var result = _.filter(data, function(i) {
    return _.includes(_.pluck(i.Instructors, "name"), "YEH, PEI HSIU")
})

return _.pluck(result, 'Course')

{% endlodash %}

They are {{result}}.