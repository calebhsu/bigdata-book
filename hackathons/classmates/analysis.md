# Analysis

{% import './data.html' as data %}

After completing the warmup exercises, your task is to do four more slightly
more challenges analyses.

## How many students like sushi as their favorite food?

{% lodash %}
return _.size(_.filter(data.comments, function(comments) {
    var clean = comments.body.toString().toLowerCase()
    return _.includes(clean, "sushi")
}))
{% endlodash %}

The answer is {{result}}.

## Who are the students liking Python the most?

{% lodash %}
var text = _.filter(data.comments, function(comments) {
    var clean = comments.body.toString().toLowerCase()
    return _.includes(clean, "python")
})
var body = _.pluck(text, "body")
return _.map(body, function(names) {
    var final = _.first(names.split('\n'))
    return final.split(': ')[1].trim()
})
{% endlodash %}

Their names are {{result}}.

## Are there more Javascript lovers or Java lovers?

{% lodash %}
var javascript = _.size(_.filter(data.comments, function(comments) {
    var clean = comments.body.toString().toLowerCase()
    return _.includes(clean, "javascript")
}))

var java = _.size(_.filter(data.comments, function(comments) {
    var clean = comments.body.toString().toLowerCase()
    if (_.includes(clean, "javascript") == false) {
        return _.includes(clean, "java")
    }
    
}))    

if (javascript > java) {
    return "JavaScript"
}
else {
    return "Java"
} 
{% endlodash %}

The answer is {{result}}.

## Who like the same food as `kjblakemore`?

{% lodash %}
return _find(data.comments, {user: {login: kjblakemore}})
{% endlodash %}

Their names are {{result}}.
