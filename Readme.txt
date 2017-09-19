After installing Sahi pro in the location "\auto\sahi_pro" do the following:

Copy the folder "salesforce" in the location "\auto\sahi_pro\htdocs\spr"

Copy the file "inject_top.txt" to the location "\auto\sahi_pro\config"

Copy the file "flex.json" to the location "\auto\sahi_pro\config\accessor_metadata"

Copy the file "donot_download_urls.txt" to the location "\auto\sahi_pro\userdata\config"

For FSA Windows:
- Please add the following function in <SahiPro>/htdocs/spr/lib.js file.
========================================================

Sahi.prototype.getSessionIds = function(title){
	var session = Packages.net.sf.sahi.session.Session;
	var sessions = session.getSessions();
	var sIds = [];
    for (var s in Iterator(sessions.values())) {
    	var sId = s.id();
    	var windowsData = s.getWindowsToJSON(1000);
    	windowsData = eval("("+windowsData+")");
    	for(var i=0; i<windowsData.length; i++){
    		var w = windowsData[i];
    		var windowTitle = w.windowTitle;
			if(title == windowTitle){
    			sIds.push(sId);
    			continue;
    		}
    	}
    }
    return sIds;
};

========================================================

- Added the following content in <ServiceMax>/js/sfmconsole-largemodern-index.html
========================================================

<!--SAHI_INJECT_START-->
<script src="http://sahi.example.com/_s_/sprc/concat.js,assert.js,listen.js,async.js,actions.js,touch.js,sfl.js,language_pack.js" id='_sahi_concat'></script>
<script src="http://sahi.example.com/_s_/dyn/SessionState_config/sahiconfig.js"></script>
<!--extra_js_placeholder-->
<!--selenium_js_placeholder-->
<!--SAHI_INJECT_END-->

========================================================
