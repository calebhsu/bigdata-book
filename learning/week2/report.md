{% import '../../hackathons/classmates/data.html' as data %}

# Report

There are {{ data.comments.length }} students who gave a self-introduction. As a
class, we brainstormed and came up with a long list of further questions we can
ask based on this data. Our team chose to tackle on the following:

# How many Applied Math majors are there?

{% lodash %}
return _.size(_.filter(data.comments, function(comments) {
    var clean = comments.body.toString().toLowerCase()
    return _.includes(clean, "applied math")
}))
{% endlodash %}

The answer is {{result}}.

# How many people submitted after August 24th?

{% lodash %}
return _.size(_.filter(data.comments, function(comments) {
    var date = comments.created_at.split('T')[0].split('-')[2]
    if (date > 24) {
        return true
    }
}))
{% endlodash %}

There were {{result}} people that submitted after August 24th.

# Who was the first person to submit Mexican food as their favorite food?

{% lodash %}
var text = _.filter(data.comments, function(comments) {
    var clean = comments.body.toString().toLowerCase()
    return _.include(clean,"mexican")
})
var body = _.pluck(text, "body")
return _.map(body, function(names) {
    var final = _.first(names.split('\n'))
    return final.split(': ')[1].trim()
})[0]
{% endlodash %}

{{result}} was the first person to submit Mexican food as their favorite food.

# How many people submitted before noon? 
{% lodash %}
return _.size(_.filter(data.comments, function(comments) {
    var time = comments.created_at.split('T')[1].split(':')[0]
    if (time < 12) {
        return true
    }
}))
{% endlodash %}

{{result}} people submitted before noon.