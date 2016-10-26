# Zendesk ST2 Integration Pack

This integration allows ticket management between StackStorm and Zendesk REST API using Zenpy python module 
Zendesk Rest API reference: https://developer.zendesk.com/rest_api/docs/core/introduction 
Zenpy python API reference: https://github.com/facetoe/zenpy



# Setup
## Configuration

* `subdomain` - zendesk subdomain name  
* `email` - Username of service account
# specify either password or token or oauth id
# you can set token or oauth at zendesk.com/agent/admin/api/settings
* `token` - API token for zendesk service account
* `password` - Password for zendesk service account
* `oauth` - oauth id for zendesk service account


## Actions

* `zendesk.update` - Update a ticket in  zendesk 
* `zendesk.insert` - Add/Insert a new ticket in  zendesk 
* `zendesk.delete` - Delete existing ticket from  zendesk 
* `zendesk.close` - Close a ticket from  zendesk with status 'closed' 

#**Example workflow using zenpack **

	$ **st2 run packs.install packs=zenpack register=all repo_url=https://github.com/techmileage/zenpack 
**...........
id: 5810691e0e8b3d326f4f2dc9
action.ref: packs.install
parameters: 
  packs:
  - zenpack
  register: all
  repo_url: https://github.com/techmileage/zenpack
status: succeeded
start_timestamp: 2016-10-26T08:28:14.964043Z
end_timestamp: 2016-10-26T08:28:37.298928Z
+--------------------------+------------------------+--------------------------+-------------------------+-------------------------------+
| id                       | status                 | task                     | action                  | start_timestamp               |
+--------------------------+------------------------+--------------------------+-------------------------+-------------------------------+
| 5810691f0e8b3d31668d05e3 | succeeded (2s elapsed) | download                 | packs.download          | Wed, 26 Oct 2016 08:28:15 UTC |
| 581069220e8b3d31668d05e5 | succeeded (2s elapsed) | virtualenv_prerun        | packs.virtualenv_prerun | Wed, 26 Oct 2016 08:28:18 UTC |
| 581069240e8b3d31668d05e7 | succeeded (8s elapsed) | setup_virtualenv         | packs.setup_virtualenv  | Wed, 26 Oct 2016 08:28:20 UTC |
| 5810692c0e8b3d31668d05e9 | succeeded (7s elapsed) | reload                   | packs.load              | Wed, 26 Oct 2016 08:28:28 UTC |
| 581069340e8b3d31668d05ec | succeeded (0s elapsed) | restart-sensor-container | packs.restart_component | Wed, 26 Oct 2016 08:28:36 UTC |
+--------------------------+------------------------+--------------------------+-------------------------+-------------------------------+


─kiran at tm1 in ~ using

	st2 action execute zenpack.insert subject='testing' description='testing zendesk'              
To get the results, execute:
 st2 execution get 5810e54f0e8b3d326f4f2dcc
╭─kiran at tm1 in ~ using
╰─○ st2 execution get 5810e54f0e8b3d326f4f2dcc
id: 5810e54f0e8b3d326f4f2dcc
status: succeeded (2s elapsed)
parameters: 
  description: testing zendesk
  subject: testing
result: 
  exit_code: 0
  **result: 22**
  stderr: "/opt/stackstorm/st2/lib/python2.7/site-packages/requests/packages/urllib3/util/ssl_.py:318: SNIMissingWarning: An HTTPS request has been made, but the SNI (Subject Name Indication) extension to TLS is not available on this platform. This may cause the server to present an incorrect TLS certificate, which can cause validation failures. You can upgrade to a newer version of Python to solve this. For more information, see https://urllib3.readthedocs.io/en/latest/security.html#snimissingwarning.
  SNIMissingWarning
/opt/stackstorm/st2/lib/python2.7/site-packages/requests/packages/urllib3/util/ssl_.py:122: InsecurePlatformWarning: A true SSLContext object is not available. This prevents urllib3 from configuring SSL appropriately and may cause certain SSL connections to fail. You can upgrade to a newer version of Python to solve this. For more information, see https://urllib3.readthedocs.io/en/latest/security.html#insecureplatformwarning.
  InsecurePlatformWarning
"
  stdout: ''

	st2 action execute zenpack.update ticket_id=22                                             
To get the results, execute:
 st2 execution get 5810e5700e8b3d326f4f2dcf

╭─kiran at tm1 in ~ using
╰─○  st2 execution get 5810e5700e8b3d326f4f2dcf
id: 5810e5700e8b3d326f4f2dcf
status: succeeded (3s elapsed)
parameters: 
  ticket_id: '22'
result: 
  exit_code: 0
  result: null
  stderr: "/opt/stackstorm/st2/lib/python2.7/site-packages/requests/packages/urllib3/util/ssl_.py:318: SNIMissingWarning: An HTTPS request has been made, but the SNI (Subject Name Indication) extension to TLS is not available on this platform. This may cause the server to present an incorrect TLS certificate, which can cause validation failures. You can upgrade to a newer version of Python to solve this. For more information, see https://urllib3.readthedocs.io/en/latest/security.html#snimissingwarning.
  SNIMissingWarning
/opt/stackstorm/st2/lib/python2.7/site-packages/requests/packages/urllib3/util/ssl_.py:122: InsecurePlatformWarning: A true SSLContext object is not available. This prevents urllib3 from configuring SSL appropriately and may cause certain SSL connections to fail. You can upgrade to a newer version of Python to solve this. For more information, see https://urllib3.readthedocs.io/en/latest/security.html#insecureplatformwarning.
  InsecurePlatformWarning
"
  stdout: '(''total tickets found: '', 1)
 ╭─kiran at tm1 in ~ using

	st2 action execute zenpack.close ticket_id=22
To get the results, execute:
 st2 execution get 5810e70a0e8b3d326f4f2dd2
╭─kiran at tm1 in ~ using
╰─○  st2 execution get 5810e70a0e8b3d326f4f2dd2
id: 5810e70a0e8b3d326f4f2dd2
status: succeeded (3s elapsed)
parameters: 
  ticket_id: '22'
result: 
  exit_code: 0
  result: null
  stderr: "/opt/stackstorm/st2/lib/python2.7/site-packages/requests/packages/urllib3/util/ssl_.py:318: SNIMissingWarning: An HTTPS request has been made, but the SNI (Subject Name Indication) extension to TLS is not available on this platform. This may cause the server to present an incorrect TLS certificate, which can cause validation failures. You can upgrade to a newer version of Python to solve this. For more information, see https://urllib3.readthedocs.io/en/latest/security.html#snimissingwarning.
  SNIMissingWarning
/opt/stackstorm/st2/lib/python2.7/site-packages/requests/packages/urllib3/util/ssl_.py:122: InsecurePlatformWarning: A true SSLContext object is not available. This prevents urllib3 from configuring SSL appropriately and may cause certain SSL connections to fail. You can upgrade to a newer version of Python to solve this. For more information, see https://urllib3.readthedocs.io/en/latest/security.html#insecureplatformwarning.
  InsecurePlatformWarning
"
  stdout: '(''Closed Ticket Status: '', <Response [200]\>)
  

### screenshot of the zendesk support ticket we worked on
![(zendesk.png)
