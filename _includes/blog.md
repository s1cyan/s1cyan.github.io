# Sending XML in a REST call with Ansible  

 

This is a short blog post that will hopefully give you a quick answer to how to send an XML body in a REST call with Ansible’s uri module.  

 

 

Ansible is a pretty modern automation engine, and as a result it expects to be handling modern content. The `uri` module in Ansible has `json`, `form-urlencoded` and `raw` as options for body format. Ansible will automatically set the Content-Type header/encode the body argument only for json and form-urlencoded, anything else you have to set yourself. 

 

**The two things you need**: 

In headers, you add the Content-Type with `application/xml`.  

In body, add your content to an xml file ( I called mine `xml_body.xml` for this example). Unfortunately, you cannot put your xml content directly in your task like you can with JSON. I’m still not a big fan of how fragmented Ansible can get so I begrudgingly put my xml in a file in templates. You do not have to specify the role it is under, Ansible will find it.  

Result: 

```
 - name: REST call w XML body 

    uri: 

      url:  

      method: PUT  

      headers: 

        Content-Type: "application/xml" 

      body: "{{lookup('template','xml_body.xml')}}" 
```

With most REST calls, you probably have some extra authentication, status code checks and etc. so add those as you need.  

 