# Grails-Application-Groovy-MimeType-Issue
To reproduce create a plain web app, perform a `generate-domain-class` along with `generate-all` for it.  At this point the app will as expected and the controller is accessible.  

Now create a `grails-app\conf\application.groovy` file and put any property in it that begins with `grails.`  Running the app now causes the content-type returned for the generated controller to be `application/xhtml+xml` instead of `text\html`.   The browser will throw an **Entity 'hellip' not defined** error with this content type.
