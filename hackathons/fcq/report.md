{% data src="fcq.clean.json" %}
{% enddata %}

# Report

As a class, we brainstormed and came up with a long list of further questions we
can ask based on the FCQ data. Out of these questions, our team chose to tackle on
the following questions. Each member on our team is reponsible for one question.

# What department should I take classes in if I want to boost my GPA? (Caleb Hsu)

{% lodash %}
var subjects = _.groupBy(data, 'Subject_Label')

var avgA = _.mapValues(subjects, function(s) {
    return _.sum(_.pluck(s, 'PCT.A')) / s.length
})

var highest =  _.last(_.sortBy(_.pairs(avgA), function(d) {
    return d[1]
}))

return highest[0]
{% endlodash %}

I should take classes in the {{result}} department if I want to boost my GPA.

# Question 2 (Name)

{% lodash %}
return "[answer]"
{% endlodash %}


# Question 3 (Name)

{% lodash %}
return "[answer]"
{% endlodash %}


# Question 4 (Name)

{% lodash %}
return "[answer]"
{% endlodash %}

# Question 5 (Name)

{% lodash %}
return "[answer]"
{% endlodash %}