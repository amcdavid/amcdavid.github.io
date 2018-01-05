# Accessing LabKey resources from the wget/curl

LabKey has good API support for most of its resources, but I recently needed to download blobs in a LabKey database (`.fcs` flow files) that didn't have any obvious API support. For some resources, LabKey will accept credentials via HTTP auth, but for others authentication occurs solely via a session cookie.  These blobs appeared to only authenticate with the session cookie.

This session cookie is called JSESSIONID, and you can look it up in Chrome->settings->cookies->details or by browsing to:
`chrome://settings/cookies/detail?site=<LABKEY SERVER URL>&search=cookie` .  Grab the JSESSIONID "content" and then add it to your wget command line:

     wget --header "Cookie: JSESSIONID=<JESSIONID CONTENT>" <URL OF LABKEY RESOURCE>
