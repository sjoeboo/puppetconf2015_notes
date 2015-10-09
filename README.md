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

json config format

official puppet module

use serverspec for checks! puppet modules add spec tests, senseu runs and reports.
I expect my puppet code to do X, thus, also prod hosts should be doing X.


Puppet 4, AIO,Puppet Collections
--------------------------------
Michael Stahnke
(started EPEL)

need confidence in automation system. set of software that works together.
opt-in upgrades (puppet3 came out folks got it that didn't intend to)
* Puppet Collections: distro for IT tooling.
  * designed for stability. who wants to MANAGE the puppet install? USE it.
  * has puppet in it
  * collections don't have breaking changes (they exist between collections)
  * consistent names for packages/services between distros
  * consistent ruby!
  * security updates. Puppet assumes risk for all things in PC/AIO
  * broken rules, so things can be consistent with ALL platforms
  * /etc = configs /var/log = logs, everything else into /opt/puppetlabs
* AIO: All in One (omnibus package):
  * augeas
  * facter
  * curl
  * dmidecode
  * hiera
  * mcollective
  * puppet
  * ruby
* Why?
  * easier.
  * batteries included
* Benefits
  * one set of docs (PE vs open source)
  * logs in one spot
  * migrations
  * legacy/security
* use git, you CAN use with github
* use puppet, you CAN use with PE. agents are the SAME.

* puppetlabs/puppet_agent module:
  * upgrades 3.8 to 4.0 agents

* Everything in AIO is opensource
* needed build system to support 70+ targets.

* Vanagon

Puppet 4, The power of puppet4
------------------------------
Example42 Martin Alfke
1 day old company

* lambdas + functions
  * slice
  * reduce
* EPP templates, use puppet syntax in templates
  * epp(template_name.epp) syntax is basically the same, no @vars
  * cli template eval. puppet epp <template>
* types , thigns are no longer pure strings
* functions can eval data types
* node inheritance no longer works.
* empty string comparison: empty string used to be false, now its true. yikes
* vars cannot start with: number. capital letter.
* vars cannot contain: dots, hyphens
* hyphers are math operators, san'e be used in module/class names

Upgrading to puppet 4: READ DOCS. READ LOGS FOR DEPS.
Setup From scratch.


10 years of puppet
------------------
cfengine isconf
puppet was originally called blink, reductive labs (ahh yes)
