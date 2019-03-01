# JOBS-Information-Extraction
Project to extract entities from Job Description Articles.

<div text-align="center">
  <img src="/images/web-demo.gif">
</div>

### Objective
Extracting information from job articles (posted by employers):

``` 
Job type:
==========================
"Full-Time, Part-Time, Contract, "Principle, temporary, .. etc"
```
```
Skills:
==========================
Soft-Skills i.e: "customer-service, vervbal communnications skills"
Technical-Skills i.e: "Java, HTTP, networking, LINUX/UNIX, C++, C#, AngularJs, javascript, bootstrap, .. etc"
```
```
Job title normalization:
==========================
Angular/Javascript Developer            ====>       Software Developers
IT Specialist Junior                    ====>       Computer User Support Specialists
Jr. Electrical Engineer                 ====>       Electrical Engineer
Sr. Electrical Engineer                 ====>       Electrical Engineer
Senior/Junior Electrical Engineer       ====>       Electrical Engineer
Full-Stack Architect/ Web Developer     ====>       Web Developers
Jr. .Net Developer                      ====>       Web Developers
Junior Business Analyst                 ====>       Business Analyst
Sr.Java Engineer                        ====>       Software Engineer
Web Developer - Internship              ====>       Web Developers
Senior Android Developer                ====>       Software Developers
UX/UI Engineer                          ====>       Software Engineers
and so on...
```
```
Years of Experiences
==========================
At least 5 years
more than 5 years
1-2 years
3+ years
5 years
and so on...
```

### DataSet
[ONET Dataset](http://opendata.cs.vt.edu/dataset/openjobs-jobpostings/resource/9a810771-d6c9-43a8-93bd-144678cbdd4a) was made public by [ONET](https://www.onetcenter.org) Organization.


### Annotation
* Built Annotation tool for semi-automation of the skills annotation. Annotaation tooks 3 weeks to annotate around 2000 job description paragraph posted by different employers.
Data preprocessing tooks one week since there was many wrong labeled data related to ONET normalized job title.

* [IOB](https://en.wikipedia.org/wiki/Inside%E2%80%93outside%E2%80%93beginning) Tagging system is followed.

```
I-TAG: Inside the chnuk
B-TAG: Beginning of the chunck
O: Outside the chunk
```

#### Used TAGS
```
B-TECH: Technical Skill (Beginning)
I-TECH: Technical skill (Inside)
B-SOFT: Soft Skill (Beginning)
I-SOFT: Soft Skill (Inside)
B-CERT: Certification (Beginning)
I-CERT: Certification (Inside)
B-YEXP: Years of Experience (Beginning)
I-YEXP: Years of Experience (Inside)
```

#### Reported wrong titles:
```
Mechanical Engineers
Pharmacist Technicians
```
Depending on the raw job title may cause ambiguity problems during the training computation even though its low computation with respect to the RNN forward and backward propagation.
To overcome such issue raw job description is used instead to construct sequence to sequence realtion between the input and the output so, more computation is needed.

### Experiments | Models Development
* LSTM Translator:
LSTM Architecture is used to translate sequence of unnormalized job title to normalized ones. good results is obtained (85% to 89 %).
* LSTM Sequence Tagger: for predicting each tokens tag
* Dataset Size: 2000 job description paragraph annotated, 65000 job title pairs for normalization module.
* Years of experience extraction module is developed by using [Spacy](http://spacy.io) functional API to extract date entities. even though some parsing rules is added (regular expressions rules) for sake of good accuracy.

### RESULT
#### JOB TITLE NORMALIZER
```
raw title:  UX/UI Engineers
normalized title:  Software Engineers
====================================================================================================
raw title:  UX/UI Designer
normalized title:  Graphic Designers
====================================================================================================
raw title:  .NET Developer
normalized title:  Web Developers
====================================================================================================
raw title:  Senior Android Engineer
normalized title:  Software Developers
====================================================================================================
raw title:  Jr Java Developer
normalized title:  Web Developers
====================================================================================================
raw title:  Sr.Java Engineer
normalized title:  Mechanical Engineers
====================================================================================================
raw title:  Senior Linux Developer
normalized title:  Software Developers
====================================================================================================
raw title:  Junior Network Engineer
normalized title:  Network And Computer Systems Administrators
====================================================================================================
raw title:  Android UI/UX Designer
normalized title:  Graphic Designers
====================================================================================================
raw title:  Android UI/UX Designer (Part-time)
normalized title:  Graphic Designers
====================================================================================================
raw title:  Part-time Android Developer
normalized title:  Software Developers
====================================================================================================
raw title:  Full-Time UI/UX Developer
normalized title:  Software Developers
====================================================================================================
raw title:  Android Developer - Internship
normalized title:  Software Developers
====================================================================================================
raw title:  Jr. Electrical Engineer
normalized title:  Electrical Engineers
====================================================================================================
raw title:  Junior Web Application Developer
normalized title:  Software Developers
====================================================================================================
raw title:  Full-stack and Frontend Engineer
normalized title:  Mechanical Engineers
====================================================================================================
raw title:  Angular/Javascript Developer
normalized title:  Web Developers
====================================================================================================
raw title:  IT Specialist Junior
normalized title:  Computer User Support Specialists
====================================================================================================
raw title:  Senior Web UI Developer
normalized title:  Software Developers
====================================================================================================
raw title:  Jr. Software Engineer (Java)
normalized title:  Software Developers
====================================================================================================
raw title:  Senior UI JavaScript Developer
normalized title:  Software Developers
====================================================================================================
raw title:  Junior Business Analyst
normalized title:  Management Analysts
====================================================================================================
raw title:  Jr Network Tech w/ Basic Cisco
normalized title:  Computer And Support Specialists
====================================================================================================
raw title:  Senior Quality Systems Specialist
normalized title:  Computer User Support Specialists
====================================================================================================
raw title:  Administrative Assistant
normalized title:  Secretaries And Administrative Assistants Except Legal Medical And Executive
====================================================================================================
raw title:  Jr. .Net Developer
normalized title:  Web Developers
====================================================================================================
raw title:  Front End Web Developer
normalized title:  Web Developers
====================================================================================================
raw title:  Full-Stack Architect/ Web Developer
normalized title:  Software Developers
```

#### SKILLS RECOGNITION
```
|Word                      |True            |Pred           |
=============================================================
|Software                  |B-TECH          |O              |
|Design                    |I-TECH          |O              |
|Engineer                  |O               |O              |
|with                      |O               |O              |
|7                         |O               |O              |
|years                     |O               |O              |
|software                  |B-TECH          |O              |
|development               |I-TECH          |O              |
|experience                |O               |O              |
|and                       |O               |O              |
|past                      |O               |O              |
|success                   |O               |O              |
|translating               |O               |O              |
|UI/UX                     |B-TECH          |B-TECH         |
|design                    |I-TECH          |I-TECH         |
|wireframes                |O               |O              |
|to                        |O               |O              |
|actual                    |O               |O              |
|code                      |O               |O              |
|If                        |O               |O              |
|you                       |O               |O              |
|have                      |O               |O              |
|produced                  |O               |O              |
|excellent                 |O               |O              |
|user                      |O               |O              |
|interfaces                |O               |O              |
|for                       |O               |O              |
|a                         |O               |O              |
|great                     |O               |O              |
|application               |O               |O              |
|we                        |O               |O              |
|would                     |O               |O              |
|love                      |O               |O              |
|the                       |O               |O              |
|chance                    |O               |O              |
|to                        |O               |O              |
|tell                      |O               |O              |
|you                       |O               |O              |
|more                      |O               |O              |
|about                     |O               |O              |
|this                      |O               |O              |
|exciting                  |O               |O              |
|opportunity               |O               |O              |
|‚Ä¢OPEN                   |O               |O              |
|TO                        |O               |O              |
|REMOTE                    |O               |O              |
|CANDIDATES                |O               |O              |
|Top                       |O               |O              |
|Reasons                   |O               |O              |
|to                        |O               |O              |
|Work                      |O               |O              |
|with                      |O               |O              |
|Us                        |O               |O              |
|Work                      |O               |O              |
|culture                   |O               |O              |
|and                       |O               |O              |
|environment               |O               |O              |
|focused                   |O               |O              |
|on                        |O               |O              |
|employee                  |O               |O              |
|well                      |O               |O              |
|being                     |O               |O              |
|exciting                  |O               |O              |
|fun                       |O               |O              |
|creative                  |O               |O              |
|and                       |O               |O              |
|client                    |O               |O              |
|focused                   |O               |O              |
|Fast                      |O               |O              |
|growing                   |O               |O              |
|company                   |O               |O              |
|with                      |O               |O              |
|opportunity               |O               |O              |
|for                       |O               |O              |
|growth                    |O               |O              |
|Work                      |O               |O              |
|with                      |O               |O              |
|a                         |O               |O              |
|collaborative             |O               |O              |
|group                     |O               |O              |
|of                        |O               |O              |
|veterans                  |O               |O              |
|and                       |O               |O              |
|novices                   |O               |O              |
|to                        |O               |O              |
|better                    |O               |O              |
|the                       |O               |O              |
|well                      |O               |O              |
|being                     |O               |O              |
|of                        |O               |O              |
|our                       |O               |O              |
|customers                 |O               |O              |
|What                      |O               |O              |
|You                       |O               |O              |
|Will                      |O               |O              |
|Be                        |O               |O              |
|Doing                     |O               |O              |
|1                         |O               |O              |
|Combine                   |O               |O              |
|the                       |O               |O              |
|art                       |O               |O              |
|of                        |O               |O              |
|design                    |O               |O              |
|with                      |O               |O              |
|the                       |O               |O              |
|art                       |O               |O              |
|of                        |O               |O              |
|programming               |O               |O              |
|2                         |O               |O              |
|Responsible               |O               |O              |
|for                       |O               |O              |
|the                       |O               |O              |
|translation               |O               |O              |
|of                        |O               |O              |
|the                       |O               |O              |
|UI/UX                     |B-TECH          |B-TECH         |
|design                    |I-TECH          |I-TECH         |
|wireframes                |O               |O              |
|to                        |O               |O              |
|actual                    |O               |O              |
|code                      |O               |O              |
|that                      |O               |O              |
|will                      |O               |O              |
|produce                   |O               |O              |
|visual                    |O               |O              |
|elements                  |O               |O              |
|of                        |O               |O              |
|the                       |O               |O              |
|application               |O               |O              |
|3                         |O               |O              |
|Work                      |O               |O              |
|with                      |O               |O              |
|the                       |O               |O              |
|Engineering               |O               |O              |
|team                      |O               |O              |
|and                       |O               |O              |
|bridge                    |O               |O              |
|the                       |O               |O              |
|gap                       |O               |O              |
|between                   |O               |O              |
|graphical                 |O               |O              |
|design                    |O               |O              |
|and                       |O               |O              |
|technical                 |O               |O              |
|implementation            |O               |O              |
|4                         |O               |O              |
|Define                    |O               |O              |
|how                       |O               |O              |
|the                       |O               |O              |
|application               |O               |O              |
|looks                     |O               |O              |
|as                        |O               |O              |
|well                      |O               |O              |
|as                        |O               |O              |
|how                       |O               |O              |
|it                        |O               |O              |
|works                     |O               |O              |
|5                         |O               |O              |
|Develop                   |O               |O              |
|new                       |O               |O              |
|user                      |O               |O              |
|facing                    |O               |O              |
|features                  |O               |O              |
|6                         |O               |O              |
|Build                     |O               |O              |
|reusable                  |O               |O              |
|code                      |O               |O              |
|and                       |O               |O              |
|libraries                 |O               |O              |
|fr                        |O               |O              |
|future                    |O               |O              |
|use                       |O               |O              |
|7                         |O               |O              |
|Ensure                    |O               |O              |
|the                       |O               |O              |
|technical                 |O               |O              |
|feasibility               |O               |O              |
|of                        |O               |O              |
|UI/UX                     |B-TECH          |B-TECH         |
|designs                   |I-TECH          |O              |
|8                         |O               |O              |
|Assure                    |O               |O              |
|that                      |O               |O              |
|all                       |O               |O              |
|user                      |O               |O              |
|input                     |O               |O              |
|is                        |O               |O              |
|validated                 |O               |O              |
|before                    |O               |O              |
|submitting                |O               |O              |
|to                        |O               |O              |
|back                      |O               |O              |
|end                       |O               |O              |
|What                      |O               |O              |
|You                       |O               |O              |
|Need                      |O               |O              |
|for                       |O               |O              |
|this                      |O               |O              |
|Position                  |O               |O              |
|7                         |O               |O              |
|years                     |O               |O              |
|of                        |O               |O              |
|software                  |B-TECH          |O              |
|development               |I-TECH          |O              |
|experience                |O               |O              |
|Proficient                |O               |O              |
|in                        |O               |O              |
|Ruby                      |B-TECH          |B-TECH         |
|on                        |I-TECH          |O              |
|Rails                     |I-TECH          |B-TECH         |
|AngularJS                 |B-TECH          |B-TECH         |
|React                     |B-TECH          |B-TECH         |
|Proficient                |O               |O              |
|in                        |O               |O              |
|HTML                      |B-TECH          |B-TECH         |
|CSS                       |B-TECH          |B-TECH         |
|Understanding             |O               |O              |
|of                        |O               |O              |
|server                    |O               |O              |
|side                      |O               |O              |
|CSS                       |B-TECH          |B-TECH         |
|platforms                 |O               |O              |
|LESS                      |O               |O              |
|SASS                      |B-TECH          |B-TECH         |
|Good                      |O               |O              |
|understanding             |O               |O              |
|of                        |O               |O              |
|AJAX                      |B-TECH          |B-TECH         |
|JSON                      |B-TECH          |B-TECH         |
|‚Ä¢                       |O               |O              |
|Nice                      |O               |O              |
|to                        |O               |O              |
|haves                     |O               |O              |
|Experience                |O               |O              |
|with                      |O               |O              |
|AWS                       |B-TECH          |B-TECH         |
|Experience                |O               |O              |
|with                      |O               |O              |
|Docker                    |B-TECH          |B-TECH         |
|or                        |O               |O              |
|other                     |O               |O              |
|container                 |O               |O              |
|based                     |O               |O              |
|platforms                 |O               |O              |
|What                      |O               |O              |
|s                         |O               |O              |
|In                        |O               |O              |
|It                        |O               |O              |
|for                       |O               |O              |
|You                       |O               |O              |
|Competitive               |O               |O              |
|salary                    |O               |O              |
|Comprehensive             |O               |O              |
|benefit                   |O               |O              |
|plans                     |O               |O              |
|401                       |O               |O              |
|k                         |O               |O              |
|matching                  |O               |O              |
|Transportation            |O               |O              |
|and                       |O               |O              |
|parking                   |O               |O              |
|benefits                  |O               |O              |
|Flexible                  |O               |O              |
|PTO                       |O               |O              |
|and                       |O               |O              |
|company                   |O               |O              |
|holidays                  |O               |O              |
|Professional              |O               |O              |
|development               |O               |O              |
|investment                |O               |O              |
|Pet                       |O               |O              |
|friendly                  |O               |O              |
|office                    |O               |O              |
|Fully                     |O               |O              |
|stocked                   |O               |O              |
|kitchens                  |O               |O              |
|with                      |O               |O              |
|drinks                    |O               |O              |
|snacks                    |O               |O              |
|and                       |O               |O              |
|coffee                    |O               |O              |
|So                        |O               |O              |
|if                        |O               |O              |
|you                       |O               |O              |
|are                       |O               |O              |
|a                         |O               |O              |
|Sr                        |O               |O              |
|Full                      |O               |O              |
|Stack                     |O               |O              |
|Engineer                  |O               |O              |
|with                      |O               |O              |
|7                         |O               |O              |
|years                     |O               |O              |
|professional              |O               |O              |
|experience                |O               |O              |
|please                    |O               |O              |
|apply                     |O               |O              |
|today                     |O               |O              |
|Required                  |O               |O              |
|Skills                    |O               |O              |
|Ruby                      |B-TECH          |B-TECH         |
|On                        |I-TECH          |O              |
|Rails                     |I-TECH          |B-TECH         |
|AngularJS                 |B-TECH          |B-TECH         |
|React                     |B-TECH          |B-TECH         |
|HTML                      |B-TECH          |B-TECH         |
|CSS                       |B-TECH          |B-TECH         |
|AJAX                      |B-TECH          |B-TECH         |
|JSON                      |B-TECH          |B-TECH         |
|LESS                      |O               |B-TECH         |
|SASS                      |B-TECH          |B-TECH         |
|AWS                       |B-TECH          |B-TECH         |
|Docker                    |B-TECH          |B-TECH         |
|UI/UX                     |B-TECH          |B-TECH         |
|JQuery                    |B-TECH          |B-TECH         |
|If                        |O               |O              |
|you                       |O               |O              |
|are                       |O               |O              |
|a                         |O               |O              |
|good                      |O               |O              |
|fit                       |O               |O              |
|for                       |O               |O              |
|the                       |O               |O              |
|Sr                        |O               |O              |
|Full                      |O               |O              |
|Stack                     |O               |O              |
|Engineer                  |O               |O              |
|Ruby                      |B-TECH          |B-TECH         |
|on                        |I-TECH          |O              |
|Rails                     |I-TECH          |O              |
|100                       |O               |O              |
|WORK                      |O               |O              |
|FROM                      |O               |O              |
|HOME                      |O               |O              |
|position                  |O               |O              |
|and                       |O               |O              |
|have                      |O               |O              |
|a                         |O               |O              |
|background                |O               |O              |
|that                      |O               |O              |
|includes                  |O               |O              |
|Ruby                      |B-TECH          |B-TECH         |
|On                        |I-TECH          |O              |
|Rails                     |I-TECH          |B-TECH         |
|AngularJS                 |B-TECH          |B-TECH         |
|React                     |B-TECH          |B-TECH         |
|HTML                      |B-TECH          |B-TECH         |
|CSS                       |B-TECH          |B-TECH         |
|AJAX                      |B-TECH          |B-TECH         |
|JSON                      |B-TECH          |B-TECH         |
|LESS                      |O               |B-TECH         |
|SASS                      |B-TECH          |B-TECH         |
|AWS                       |B-TECH          |B-TECH         |
|Docker                    |B-TECH          |B-TECH         |
|UI/UX                     |B-TECH          |B-TECH         |
|JQuery                    |B-TECH          |B-TECH         |
|and                       |O               |O              |
|you                       |O               |O              |
|are                       |O               |O              |
|interested                |O               |O              |
|in                        |O               |O              |
|working                   |O               |O              |
|the                       |O               |O              |
|following                 |O               |O              |
|job                       |O               |O              |
|types                     |O               |O              |
|Information               |O               |O              |
|Technology                |O               |O              |
|Engineering               |O               |O              |
|Professional              |O               |O              |
|Services                  |O               |O              |
|Within                    |O               |O              |
|the                       |O               |O              |
|following                 |O               |O              |
|industries                |O               |O              |
|Computer                  |O               |O              |
|Software                  |O               |O              |
|Our                       |O               |O              |
|privacy                   |O               |O              |
|policy                    |O               |O              |
|Your                      |O               |O              |
|resume                    |O               |O              |
|and                       |O               |O              |
|information               |O               |O              |
|will                      |O               |O              |
|be                        |O               |O              |
|kept                      |O               |O              |
|completely                |O               |O              |
|confidential              |O               |O              |
|Looking                   |O               |O              |
|forward                   |O               |O              |
|to                        |O               |O              |
|receiving                 |O               |O              |
|your                      |O               |O              |
|resume                    |O               |O              |
|through                   |O               |O              |
|our                       |O               |O              |
|website                   |O               |O              |
|and                       |O               |O              |
|going                     |O               |O              |
|over                      |O               |O              |
|the                       |O               |O              |
|job                       |O               |O              |
|in                        |O               |O              |
|more                      |O               |O              |
|detail                    |O               |O              |
|with                      |O               |O              |
|you                       |O               |O              |
|CyberCoders               |O               |O              |
|Inc                       |O               |O              |
|is                        |O               |O              |
|proud                     |O               |O              |
|to                        |O               |O              |
|be                        |O               |O              |
|an                        |O               |O              |
|Equal                     |O               |O              |
|Opportunity               |O               |O              |
|Employer                  |O               |O              |
|All                       |O               |O              |
|qualified                 |O               |O              |
|applicants                |O               |O              |
|will                      |O               |O              |
|receive                   |O               |O              |
|consideration             |O               |O              |
|for                       |O               |O              |
|employment                |O               |O              |
|without                   |O               |O              |
|regard                    |O               |O              |
|to                        |O               |O              |
|race                      |O               |O              |
|color                     |O               |O              |
|religion                  |O               |O              |
|sex                       |O               |O              |
|national                  |O               |O              |
|origin                    |O               |O              |
|disability                |O               |O              |
|protected                 |O               |O              |
|veteran                   |O               |O              |
|status                    |O               |O              |
|or                        |O               |O              |
|any                       |O               |O              |
|other                     |O               |O              |
|characteristic            |O               |O              |
|protected                 |O               |O              |
|by                        |O               |O              |
|law                       |O               |O              |
|Your                      |O               |O              |
|Right                     |O               |O              |
|to                        |O               |O              |
|Work                      |O               |O              |
|‚Äì                       |O               |O              |
|In                        |O               |O              |
|compliance                |O               |O              |
|with                      |O               |O              |
|federal                   |O               |O              |
|law                       |O               |O              |
|all                       |O               |O              |
|persons                   |O               |O              |
|hired                     |O               |O              |
|will                      |O               |O              |
|be                        |O               |O              |
|required                  |O               |O              |
|to                        |O               |O              |
|verify                    |O               |O              |
|identity                  |O               |O              |
|and                       |O               |O              |
|eligibility               |O               |O              |
|to                        |O               |O              |
|work                      |O               |O              |
|in                        |O               |O              |
|the                       |O               |O              |
|United                    |O               |O              |
|States                    |O               |O              |
|and                       |O               |O              |
|to                        |O               |O              |
|complete                  |O               |O              |
|the                       |O               |O              |
|required                  |O               |O              |
|employment                |O               |O              |
|eligibility               |O               |O              |
|verification              |O               |O              |
|document                  |O               |O              |
|form                      |O               |O              |
|upon                      |O               |O              |
|hire                      |O               |O              |
|Ruby                      |B-TECH          |B-TECH         |
|On                        |I-TECH          |B-TECH         |
|Rails                     |I-TECH          |B-TECH         |
|AngularJS                 |B-TECH          |B-TECH         |
|React                     |B-TECH          |B-TECH         |
|HTML                      |B-TECH          |B-TECH         |
|CSS                       |B-TECH          |B-TECH         |
|AJAX                      |B-TECH          |B-TECH         |
|JSON                      |B-TECH          |B-TECH         |
|LESS                      |O               |B-TECH         |
|SASS                      |B-TECH          |B-TECH         |
|AWS                       |B-TECH          |B-TECH         |
|Docker                    |B-TECH          |B-TECH         |
|UI/UX                     |B-TECH          |B-TECH         |
|JQuery                    |B-TECH          |B-TECH         |
```
