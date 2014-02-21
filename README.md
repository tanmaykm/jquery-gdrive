# JQuery Plugin for Google Drive API

Google Drive is a nice and easy (once you get used to it) way to store and share files on the cloud. Apps on Android phones and tablets synchronize their documents and images to Google Drive. One can think of so many interesting applications using them.

Such applications often need to let the user choose files and folders from their Google Drive, read their contents and do something useful. This simple JQuery plugin provides APIs for some often used operations.

### Setting up jquery-gdrive
- Download the file `jquery-gdrive.js` and include it in your HTML.
- Include the following code snippet in your HTML (after modifying it appropriately of course):


````
    
 <script src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
 <script src="//apis.google.com/js/client.js"></script>
 <script src="jquery-gdrive.js"></script>
 <script type="text/javascript">
   $(document).ready(function() {
     $().gdrive('init', {
       'devkey': 'YOUR GOOGLE DEVELOPMENT KEY HERE',
       'appid': 'YOUR GOOGLE APPLICATION ID HERE'
 });
 </script>
````

### Authenticating to Google
The plugin handles authentications and authorizations required from Google. The user is prompted for permissions on first use (in a session). The application can retrieve the authenticated user id and access token as below:

````
// returns the user id (e-mail) which is signed in.
user_id = $().gdrive('user')

// returns the authorization token
auth_tok = $().gdrive('token')
````

If authentication is delegated to be done by `jquery-gdrive`, any additional authentication scopes required by the application can be provided through the `init` call using the `scope` option (similar to how `devkey` and `appid` are supplied).

If authorization is done by the application instead, the results can be shared with jquery-gdrive through the `init` call using options authtok (for authorization token) and user (for authorized email id).


### Selecting Files and Folders

jquery-plugin uses Google Drive `picker` API to display a file picker dialog. Selection made in the file picker can be populated in an HTML element or returned via a callback.

Configure HTML elements that should hold selected Google Drive files using something similar to the snippet below.

````
// gdrive_file is the HTML elelemt that will hold the selection result
$('#gdrive_file').gdrive('set', {

	// Trigger is the HTML element which on clicking should show the picker 
	// (defaults to the same element that hosts the result)
	'trigger': 'gdrive_file_selector', 
	
	// Text to show as header of the picker dialog
	'header': 'Select a file',
	
	// File/folder types to be shown and selected.
	// Use 'application/vnd.google-apps.folder' for folder.
	// Complete list here: https://developers.google.com/drive/web/mime-types
	// Defaults to showing all.
	'filter': ''
});
````

The selected files are assigned an URL with a custom `gdrive` scheme with format `gdrive://<file_name>/<file_id>`.


### Try it

Try the API with a sample implementation [here](http://tanmaykm.github.io/jquery-gdrive/jquery-gdrive.html).

Or download the repository, run any simple static file web server, e.g. `python -m SimpleHTTPServer 8080` to start a simple web server, point your browser to [http://localhost:8080/](http://localhost:8080/test/jquery-gdrive.html)


### TODO
- read/write/modify files
- create folders
- events
