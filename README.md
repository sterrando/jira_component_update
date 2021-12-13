# jira_component_update
This is a simple tool in order to load components (component name:component description) to JIRA instance using the REST API. 

Tested with API Rev. 2.

The usage is straightforward: 

* Create a jira_component_tools instance providing your Jira username, passCODE, project name, URL. The uri is optional and defaults to ```/rest/api/2/search```. Everything is a string.
* Call the ```log_in()``` method
* Upload the components with the ```load_components()``` method, passing a dictionary in the form ```{name:description}```

Example of parsing an excel file and uploading (replace your credentials and filename):

```python
    ### EXAMPLE: LOAD COMPONENTS FROM EXCEL WORKBOOK ###
    #
    #   Format: 
    #       Column A: NAME
    #       Column B: DESCRIPTION
    #    
    from openpyxl import load_workbook
    wb = load_workbook( filename = "components.xlsx" )
    ws = wb['Sheet1']
    i = 2
    component_dict = {}        
    while (ws['A'+str(i)].value):        
        try:
            name = str(ws['A'+str(i)].value)
            desc = str(ws['B'+str(i)].value)              
            component_dict[name] = desc
        except:
            pass
        i += 1
    #
    ###################################################
    
    jira_url = r"https://YOURURL.atlassian.net"    
    auth_user = "YOURUSERNAME"
    auth_pwd = "YOURPASSWORD"
    project = "YOURPROJECT"
    
    j=jira_component_tools(auth_user,auth_pwd,project,jira_url)
    j.log_in()
    j.load_components(component_dict)
```
