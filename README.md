# Grails-Application-Groovy-MimeType-Issue
To reproduce create a plain web app, perform a `generate-domain-class` along with `generate-all` for it.  At this point the app will as expected and the controller is accessible.  

Now create a `grails-app\conf\application.groovy` file and put any property in it that begins with `grails.`  Running the app now causes the content-type returned for the generated controller to be `application/xhtml+xml` instead of `text\html`.   The browser will throw an **Entity 'hellip' not defined** error with this content type.

**Note:** I discovered this while using the new spring security core plugin, since it generates an application.groovy file with several grails.* settings, but the plugin is not required to recreate the issue.

**Additional info:**  Not sure if this is related, but logging the runtime value of `grailsApplication.config.get( 'grails.mime.types' )` shows that the order of the values is effected when an application.groovy file is merged that contains `grails.` properties.

**mimeTypes order when application.groovy contains NO `grails.` properties**

    all:*/*,
    atom:application/atom+xml,
    css:text/css,
    csv:text/csv,
    form:application/x-www-form-urlencoded,
    html:[text/html,application/xhtml+xml],
    js:text/javascript,
    json:[application/json,text/json],
    multipartForm:multipart/form-data,
    pdf:application/pdf,
    rss:application/rss+xml,
    text:text/plain,
    hal:[application/hal+json,application/hal+xml],
    xml:[text/xml,application/xml],
    html[1]:application/xhtml+xml,
    xml[1]:application/xml,
    hal[0]:application/hal+json,
    json[0]:application/json,
    hal[1]:application/hal+xml,
    html[0]:text/html,
    xml[0]:text/xml,
    json[1]:text/json

**mimeTypes order when application.groovy contains `grails.` properties**

    html[1]:application/xhtml+xml,
    csv:text/csv,
    text:text/plain,
    css:text/css,
    xml[1]:application/xml,
    hal[0]:application/hal+json,
    rss:application/rss+xml,
    js:text/javascript,
    json[0]:application/json,
    pdf:application/pdf,
    form:application/x-www-form-urlencoded,
    atom:application/atom+xml,
    hal[1]:application/hal+xml,
    html[0]:text/html,
    all:*/*,
    xml[0]:text/xml,
    json[1]:text/json,
    multipartForm:multipart/form-data,
    html:[text/html,application/xhtml+xml],
    json:[application/json,text/json],
    hal:[application/hal+json,application/hal+xml],
    xml:[text/xml,application/xml] 
