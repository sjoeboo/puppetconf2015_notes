# puppetconf2015_notes
Notes from Puppetconf2015

Thursday 10.8.2015
==================

Keynote: Luke Kanies
--------------------
"Local, Organic, Artisinal Devops" aka, Portland

* 30K companies, 22 a day start using puppet for the first time
* 3500 modules in the forge
* 1000 paying customers
* 400 employees

Everyone is looking for their own bridge to live under.
Devops is still mostly a theory. Rename sys admins to Devops engineers.
Can't add quality @ the end. Add quality in the process. Evol backwards from the customer.
Incremental bits of automation.

Puppet Application Orchestrator:
Ryan Coleman:
you can get a lot done with puppet, core infra, app infra, app releases....
* Elevating Puppet:
  * Node Level:
    * Composition (core configs, ldap, ntp, etc etc)
    * Flexability(fact based, move around, resue)
    * Predicability (noop mode etc)
    * Orchestration (relationships)
  * App level:
    * exported resources = multiple runs.
    * want to fix that "bug" ^^^ (eventually consistent)
    * services are center of Orchestrator
    * who provides what + dependancies of those services
    * your database server knows how things need to connect to it.
    * let the apps consume this data
    * context
    * export/consume (not relationships, but what service need/provide)

  Orchestrator lays ground work for next 10 years

  * goal:  to the be the spin of the application deployment infra.
  * orch + direct puppet = canary host automation
  * gradual deployment

Infrastructure as Code & Monitoring
-----------------------------------
Sean Porter, Heavy Water Ops. @portertech

What infra as code ? Enable th rebuilding/reconstructing of the bussiness form nothing but a source code repository.

move tests close to code, before review/build pipeline.

serverspec: rspec tests for servers
kitche-puppet
vagrant-serverspec

sensu, designed for CM systems (puppet etc)
designed for dynamic infra. public networks. automatic deregistration
rabbit mq. servers= event processors, client = things runnig checks. redis backend.

service checks, simple to write and understand. stdout + exit codes. can have formatted metrics, send to various backends (graphite etc)
top to bottom service dep chain.

local socket allow scripts etc to check in and sendstatus, with ttl, aka, deadmans switch

check -> filters -> mutators -> handlers
github.com/sensu-plugins
monitoring-plugins.Organic

json config formatted

official puppet module

use serverspec for checks! puppet modules add spec tests, senseu runs and reports.
I expect my puppet code to do X, thus, also prod hosts should be doing X.
