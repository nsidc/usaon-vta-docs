# Glossary

* `Survey`: A solicitation for input from a `Respondent`. 
* `Response`: A completed survey.
* `Library`: The collection of all `responses`.
* `Registry`: The collection of available `survey objects` for use in `responses`.
* `Analysis`: The process of converting many survey responses to a Sankey diagram by an
  `Analyst` interacting with the `Library`. Surveys are searched by title, `tags`, and/or other survey object fields.


## Response Object Registry

A list of available `response objects`. Drives consistency in naming across `surveys` to
support `analysis` and also to ease data entry for `Respondents`, over time.

`Respondents` may add new `applications`, `data products`, and `observing systems` to the `registry`.

There is a generic `Registered Survey Object` structure that applies to Applications, 
Data Product, and Observing Systems. There is a separate structure to register 
`Societal Benefit Area objects`.

Ongoing efforts are being made to align this data structure with best practices and partner organization
structures (e.g. Polar Observing Assets working group, Arctic Data Center, Federated 
Search crew) with the goal to be able to import or sync items in the registry 
from an external source.


### Fields


* `Object Type`: Type of Object - `Observing System`, `Data Product`, or `Application`
* `Short Name`: Short name/description of object, which would be displayed in the analysis to save space.
* `Full Name`: Full name of the object, which can be left blank if it is the same as the `short name`
* `Organization`: The entity responsible for operation of the observing system, data product, or application.
  It would be best to use standard names: https://ror.readme.io/docs/create-ror-powered-typeaheads-in-forms
* `Funder`: The entity responsible for funding the observing system, data product, or application. 
  It would be best to use standard names: https://ror.readme.io/docs/create-ror-powered-typeaheads-in-forms
* `Country/Countries`: The countries contributing to running or funding an object. Use ISO 3166.
* `Website`: The URL to access the referenced object directly
* `Description`: Short summary of the object, including geographic or thematic scope. This could also be 
  referred to as an abstract (see Arctic Data Center). 
* `Contact Name`: The name of a point of contact for the object, e.g. a data manager or program coordinator.
* `Contact Title`: The title of a point of contact for the object.
* `Contact Email`: The email address for a point of contact for the object.
* `Tags`: This is a user-defined field that admins can and will edit. It creates additional flexibility in 
  the analyis, for example allowing for a regionally- or thematically-focused `analysis`.
* `Version`: This field allows the `analyses` to reflect updates overtime. Likely
  this field will have to be open text so it can match the versioning information that the organization uses.
* `Persistent Identifier`: A standard way to refer back to the object's source, usually a ROR or DOI

`Application` objects also include:
* `Application Performance Criteria`: Text description of what the ideal performance of this data
  product looks like.

  _NOTE_ We intend to do `current state` and `desired state` `analyses`. In a `desired state` `analysis` we
  would need a way to include `desired state` objects, for instance the USGS stream gage network if
  funding increased and there were X number of additional gages. This would allow us to trace the impact
  of changes on the entire network. Would we do this as another type of `version`, via specific `tags`,
  and/or through unique naming conventions. Related to the survey `type`.

## Rated Instance of an Object

The rating answers two questions - how important is a particular `Observing System`, 
`Data Product`, or `Application`and how well does it perform. It is reflected in the 
`analysis` by the thickness and color of the link connecting two `survey objects`. For 
instance: Imagine a satelite (`observing system`) that is very important to a sea ice 
`data product` but performs poorly because of persistent Arctic cloud cover and high 
latency (`gaps`. Those would be linked by a thick (high `criticality`) red (low 
`performance`) line. 

Response objects exist both as a definition in the `registry` and an instantiation with
rating(s) and other fields associated with a `response`. The following specifications
pertain to rated instances, _not_ `registry` definitions.

* `Link`: Defines which `survey objects` are connected. The rating is applied to that `link`.
* `Performance rating`: 0-100 rating of the performance of the subject. Answers the question: 
  What is your satisfaction with this input? (0=No performance, 100 = perfect)
* `Criticality rating`: 0-10 rating of the criticality of an input to an output,
  e.g. criticality of an `observing system` to a `data product`. This answers the question:
  On a scale of 1-10, how much would the loss of this input impact the performance of your 
  `data product` or `application` (1 - very little impact; 10 - complete loss of performance).
* `Rationale`: Why a `criticality` or `performance` rating was selected.
* `Gaps`: If the rating is less than "ideal" what improvements are needed.
* `Variable or Attribute`: If an `observing system` or `data product` contains many
  observable properties or variables, this allows a `respondent` to specify
  which field they used. 
* `Rated by`: Link to the `respondent` who provided this rating.

The `node color` of an `observating system` or a `data product` is defined in this 
document: https://docs.google.com/presentation/d/1RmEGcPkC3_9o3qeAndv0QvAcdZwFIHC-/edit#slide=id.g1e651286dde_0_54
The `node color` of an `application` is rated separately based on the application performance
compared to the `application performance criteria`.

## Surveys

* `ID`: Computer generated identifier
* `Name`: Unique name of survey
* `Description`: Narrative description of the survey topic 
* `Type`: Surveys could be requesting information about the current state or a hypothetical future
  state (desired state) of `response objects`.
* `Tags`: This is a user-defined field that admins can and will edit. It creates additional flexibility in 
  the analyis, for example allowing for a regionally- or thematically-focused `analysis`.
* `Year`: Allows for repeated analyses to show change over time
* `Status`: Published or unpublished
* `Respondents`: List of `respondents` with edit-access
  
While most `surveys` will link observing systems, data products, applications, and societal benefit areas, 
some may simply allow for a data manager to link the `data product` to `observing systems` without any related `application`.

### Responses

* `Respondents`: `Experts` who can contribute to `response`.
* `Tags`: Arbitrary strings for grouping surveys. For example: `river-watch`.
* `Version`: Surveys can be re-issued, with changes, as a new version. E.g. a new survey
  is created as version "1" (version may be represented to user as creation date).
  Later, the survey is copied to version "2", altered, and re-issued, possibly to a
  different `respondent`. We also copy the old response to the new version so the
  `respondent(s)` do not need to start from scratch.
* `Validated date`: Date when an admin marked this survey valid for inclusion in the
  `library`.
* `Status`: Draft, ready to validate, validated, ??? (_TODO_: Better to use date fields
  instead? e.g. a submitted response has `submitted_date` populated, a draft does not)



### Response objects 

_NOTEfromHAZEL_ I believe this section is out of date, and the Rated Instance of 
an Object is sufficient and up-to-date. 

Response objects exist both as a definition in the `registry` and an instantiation with
rating(s) and other fields associated with a `response`. The following specifications
pertain to rated instances, _not_ `registry` definitions.

Some field definitions that may apply to multple objects:

* `Performance rating`: 0-100 rating of the performance of the subject
* `Criticality rating`: 0-100 (or less) rating of the criticality of an input to an output,
  e.g. criticality of an `observing system` to a `data product`. Rating must not be
  greater than the `performance rating` of the ouptut subject.
* `Rationale`: Why a `criticality` or `performance` rating was selected.
* `Gaps`: Areas where improvement is needed.


#### Observing system

The optional input to a `Data product` (e.g. reanalysis or model-derived data products
may not require an observing system).

Fields/relationships:

* `Performance rating`
* `Rationale` for performance rating
* `Gaps`
* `Data product(s)` supported by this observing system
    * `Criticality rating`
    * `Rationale` for criticality rating


#### Data product

* `Performance criteria`: Text description of what the ideal performance of this data
  product looks like. (_TODO_: Needs more thought. There is some disagreement on the AON
  side about how/if this should be used.)
* `Performance rating`
* `Rationale` for performance rating (_NOTE_: AON team to consider if pre-defined values
  are a good idea.)
* `Gaps`
* `Application` supported by this data product (always the same for a given survey,
  since each survey corresponds with exactly 1 application)
    * `Criticality rating`
    * `Rationale` for criticality rating


#### Application

* `Performance criteria`: Text description of what the ideal performance of this data
  product looks like.
* `Performance rating`
* `Rationale` for performance rating
* `Gaps`


#### Societal Benefit Area (SBA)

This response subject may be completed by more than one `respondent`, with the option to visualize
an aggregated/averaged view or individual `responses`. 

* `Application` being rated in association with this SBA:
  * `Performance rating`
  * `Rationale` of performance rating
  * `Criticality rating`
  * `Rationale` of criticality rating
  * `Gaps` needed improvements
 

### Application survey

Gather information about `application(s)` and its related `data products` and
their related `observing systems`.


### Societal Benefit Area survey

Gather information about Societal Benefits of an application. Related to exactly 1
`Application survey`.

This type of survey generally requires input from a larger group. For example, a SBA
survey may be sent to up to ~20 `respondents` known as a `societal benefit cohort` and
request information about how 1-3 specific `SBAs` relate to the `application`. Multiple
SBA surveys will be needed to fill out all societal benefits of an application.


## Analysis

A visualization that is generated from the `library` of responses by an `Analyst`
selecting filters based on fields of `response objects`, such as `tags`. We envision
being able to blend `responses` around common Objects or Fields within those Objects, for
example: "show all `responses` tied to a given `data product`". Or "show all where `tags`
include 'rivers'", etc.

* `Name`: Unique
* `Description`
* `Analyst`
* Filter criteria or list of `responses` associated with the analysis. (_TODO_: If we
  don't want an analysis to change over time, we should probably link it to `reponses`
  by ID. But if we _do_ want the analysis to be automatically updated as more
  `responses` are submitted with e.g. a specific `tag`, we should use filter criteria)


## User personas / roles

### Admin

A user who creates a `survey` and invites `experts` to respond, in addition to
validating `responses` and marking them valid/complete.

When creating a `survey`, the admin either creates or selects an `application` in the
registry to associate with the survey.

Can create `surveys` by creating new `versions` of old surveys.

Fields/relationships:

* `Name`
* `Email`
* `ORCID iD`
* `Surveys created`
* `Affiliation`
* `Biography`


### Respondent (field expert)

A user who is invited to register to provide a `response` to a `survey`. Admins will
assign Surveys to Experts. Experts can contribute to multiple Surveys; Surveys can have
many Experts. 

Experts may add new `applications`, `data products`, and `observing systems` to the 
`registry`, or may select existing `objects`.

Fields/relationships:

* `Name`
* `Email`
* `OrcID` 
* `Biography`
* `Affiliation` (should this be saved on a response-by-response basis? Affiliation may
  change between surveys)
* `Tags` of interest (areas of expertise, e.g. `river-watch`, `hydrology`)
* `Responses` submitted


### Analyst

These are people who are viewing the data. Not contributing to it in any way.
A user who registers to generate one or more `analysis`. Eventually, we’d like Analysts
to be able to save their Analyses, recreate them and update them. I’m not sure we need
or should track things like Orcid ID, Bio, Affiliation for Analysts, but we could give
them option. It would help with our analytics.

We might also need to support a Guest Analyst so someone could do visualizations without
registering. If we don’t want to create user accounts, then basically everyone would be
a Guest Analyst and they could just export .jpgs and JSON to recreate their analyses.

Fields/relationships:

* Name
* OrcID (optional?
* Biography
* Affiliation
* Tags of interest (areas of expertise, e.g. `river-watch`)
* `Analyses` submitted


### SBA Rating Cohort

A group of `respondents` who provide `responses` to `surveys` focused on SBA ratings. A cohort
will generally be solicited to complete many `Societal Benefit surveys`, focusing on a
small number of `SBAs`, to provide a view of the societal benefits of many
`applications`.

Fields/relationships:

* `Name`: Unique
* `Description`
* `Expert(s)`: Members of cohort
