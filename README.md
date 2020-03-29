# CASA Project & Organization Overview
[![Build Status](https://travis-ci.org/ruby4good/casa.svg)](https://travis-ci.org/ruby4good/casa)

CASA (Court Appointed Special Advocate) is a role fulfilled by a trained volunteer sworn into a county-level juvenile dependency court system to advocate on behalf of a youth in the corresponding county's foster care system. CASA is also the namesake role of the national organization, CASA, which exists to cultivate and supervise volunteers carrying out this work – with county level chapters (operating relatively independently of each other) across the country. 

<strong>PG CASA (Prince George's County CASA in Maryland) seeks a volunteer management system to:</strong>
- provide volunteers with a portal for logging activity
- oversee volunteer activity 
- generate reports on volunteer activity

<strong>How CASA works:</strong>
- Foster Youth (or case worker associated with Foster Youth) requests a CASA Volunteer.
- CASA chapter pairs Youth with Volunteer.
- Volunteer spends significant time getting to know and supporting the youth, including at court appearances. 
- Case Supervisor oversees CASA Volunteer paired with Foster Youth and monitors, tracks, and advises on all related activities.
- At PG CASA, the minimum volunteer commitment is one year (this varies by CASA chapter, in San Francisco the minimum commitment is ~ two years). Many CASA volunteers remain in a Youth's life well beyond their youth. The lifecycle of a volunteer is very long, so there's a lot of activity for chapters to track!

<strong>Why?</strong>
Many adults circulate in and out of a Foster Youth's life, but very few of them (if any) remain. CASA volunteers are by design, unpaid, unbiased, and consistent adult figures for Foster Youth who are not bound to support them by fiscal or legal requirements. 

<strong>Project Terminology</strong>
- Foster Youth = _Case_
- CASA Volunteer = _Volunteer_
- Case Supervisor = _Case Supervisor_
- CASA Administrator = _Superadmin_

<strong>Project Considerations</strong>
- PG CASA is operating under a very tight budget. They currently _manually input volunteer data_ into <a href="http://www.simplyoptima.com/">a volunteer management software built specifically for CASA,</a> but upgrading their account for multiple user licenses to allow volunteers to self-log activity data is beyond their budget ($0). Hence why we are building as lightweight a solution as possible that can sustain itself on Microsoft Azure nonprofit credits for hosting (totalling $3,500 annually).
- While the scope of this platform's use is currently only for PG County CASA, we are building with a mind toward multitenancy so this platform could prospectively be used by CASA chapters across the country. We consider PG CASA an early beta tester of this platform. 

<p><strong>More information:</strong></p>
<p><a href="https://pgcasa.org/">Learn more about PG CASA here.</a></p>
<p><a href="https://pgcasa.org/volunteer-description/">You can read the complete role description of a CASA volunteer in Prince George's County here.</a></p>


### Setup to develop:

1. install a ruby version manager: [rvm](https://rvm.io/) or [rbenv](https://github.com/rbenv/rbenv)
1. when you cd into the project diretory, let your version manager install the ruby versionin .ruby-version
1. gem install bundler
1. bundle install
1. bundle exec rails test 
1. bundle exec rails server # run server

#### One-time already-done project setup (for historical reference)

1. install a ruby version manager: rvm or rbenv
1. rvm install ruby 2.7.0 # should be auto-installed when you cd into the casa directory because of .ruby-version
1. gem install bundler
1. bundle install
1. rails new . -d postgresql --webpacker react
1. [brew install postgres](https://wiki.postgresql.org/wiki/Homebrew) OR brew postgresql-upgrade-database (if you have an older version of postgres)
1. rails db:create # requires running local postgres
1. rake app:update:bin # required for scaffold to not hang
1. rails generate scaffold CasaCase case_number:string teen_program_eligible:boolean
1. rails webpacker:install # required for rails to run
1. rake db:migrate
1. brew install yarm # because of error: Yarn not installed. Please download and install Yarn from https://yarnpkg.com/lang/en/docs/install/
1. rails server
1. 
1. 
1. 
1. 
1. 




TODO:

missing react????

Add CI

rails generate devise:install
rails generate devise user
rails db:migrate
rails generate devise:views


casa: name
all_casa_admin: email, name, hashed_password(devise)
user: email, name, casa_id, hashed_password(devise), role(enum: inactive, volunteer, supervisor, casa-admin)
supervisor_volunteer: volunteer_user_id, supervisor_user_id
supervisor_case: supervisor_user_id, case_id
case_assignment: volunteer_user_id, case_id, is_active - since multiple volunteers can be assigned to the same case in different quarters
case: case#, teen_program_eligible
case_update: user_id, case_id, (since a volunteer can switch cases or have multiple), update_type. (youth, school, social worker, therapeutic agency worker contact, therapist, attorney, bio-parent, foster parent, other family contact, supervisor, court, other), other_type_text
uploaded_import: import_json (only saved fields?) maybe don't do this at all, in-memory only
