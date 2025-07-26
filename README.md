# Vimeo LMS Integration: SCORM & xAPI Guidance

As means of guidance on integrating Vimeo video content with Learning Management Systems (LMS) through SCORM and xAPI standards, this repository explains the practical steps for enterprise account holders to set up e-learning preferences, export SCORM packages, and enable learners to engage with Vimeo content within an LMS.

---

## Understanding the integration process

Integrating Vimeo content with an LMS involves specific packaging and communication methods, rather than direct display. The following sections detail the core procedures and interactions.

### Setting up default LMS preferences

The initial configuration of general LMS preferences within your Vimeo account includes setting up learner management, choosing technical standards (SCORM 1.2, SCORM 2004 v3, xAPI, AICC, cmi5), selecting scoring methods (percentage watched, pass/fail), and defining completion percentage thresholds. Please note that Learner IDs, sent from the LMS to Vimeo via SCORM packages, are linked to Vimeo users, especially when Single Sign-On (SSO) is in use.

<img width="734" height="709" alt="image" src="https://github.com/user-attachments/assets/df392ad8-5699-40b2-9b7e-81f8411d0647" />


### SCORM export and LMS integration
A Vimeo Export Service, which is a backend component, creates the SCORM ZIP file. The LMS handles the import and publishing of this package within its own system.

<img width="1129" height="553" alt="image" src="https://github.com/user-attachments/assets/4758a5a9-b247-4e84-b041-2ddbf65f6085" />



### Learner accessing Vimeo content within the LMS
The embedded Vimeo content is the player displayed inside the LMS, while the Vimeo Playback Service manages video streaming and logging from Vimeo's servers. Scoring is determined by your chosen methods, and the LMS controls how many times a learner can resubmit.

<img width="1187" height="637" alt="image" src="https://github.com/user-attachments/assets/1d585ded-c354-44f6-8542-6b3578b78c94" />


### The SCORM/xAPI integration package explained
The downloadable ZIP file from Vimeo acts as a complete integration package, adhering to either SCORM or xAPI e-learning standards. This package is specifically designed for use by an LMS, providing it with all the necessary instructions and information for seamless integration and tracking of the associated Vimeo content.

When you upload this ZIP file, the LMS unpacks and interprets its contents. This package gives the LMS the exact details and commands needed to correctly start and show the Vimeo video player within its own system. It is important to remember that the actual video content remains on Vimeo's dedicated servers. The SCORM/xAPI package within the ZIP file typically contains a secure link or embed code. When the LMS processes this, it instructs the system to display the Vimeo video player, which then streams the video directly from Vimeo.

The LMS then creates an interface within the course module, often appearing as an embedded player or a clickable link that opens the video. This interface allows the learner to engage with the Vimeo video. Crucially, the SCORM/xAPI communication protocols built into the package enable a continuous exchange of data between the Vimeo player and the LMS. This two-way communication allows the LMS to accurately record and receive comprehensive data about the learner's viewing progress and completion status, which is then used for accurate grading and full performance tracking.

<img width="1212" height="670" alt="image" src="https://github.com/user-attachments/assets/d1498102-e275-497f-8b25-2d67a145c46a" />


### Further information
About xAPI (Placeholder for your initial article)

---

UML 1.
@startuml
title Configure Default LMS Settings - Vimeo Internal Process
box "Vimeo" #LightBlue
  participant "Vimeo Account" as VimeoInterface
  database "Vimeo Database" as VimeoDB
end box

VimeoInterface -> VimeoInterface : Manages navigation to Team Settings
VimeoInterface --> VimeoInterface : Displays team settings page
VimeoInterface -> VimeoInterface : Handles scrolling to "E-learning" section
VimeoInterface --> VimeoInterface : Displays E-learning options
VimeoInterface -> VimeoInterface : Processes Learner Management configuration (views Learner IDs)
Note over VimeoInterface, VimeoDB
Learner IDs passed from LMS to Vimeo via SCORM packages.
If SSO is used, Vimeo associates Learner IDs with Vimeo users.
End Note
VimeoInterface -> VimeoInterface : Registers selection of Technical Standard (SCORM 1.2, SCORM 2004 v3, xAPI, AICC, cmi5)
VimeoInterface -> VimeoInterface : Registers selection of Scoring Method (Percentage watched, Pass/fail)
VimeoInterface -> VimeoInterface : Registers setting of Completion Percentage Threshold
VimeoInterface -> VimeoDB : Submits and stores default E-learning settings
VimeoDB --> VimeoInterface : Confirms settings saved
VimeoInterface --> VimeoInterface : Updates settings confirmation
@enduml

---

UML 2.
@startuml
title Integrate Videos with LMS (SCORM Export)

actor "Enterprise Account Owner/Admin/Contributor" as User
box "Vimeo System" #LightBlue
    participant "Vimeo Platform" as Vimeo
end box
participant "Learning Management System (LMS)" as LMS

User -> Vimeo : Navigates to video library & settings
Vimeo --> User : Displays video options

User -> Vimeo : Requests SCORM package export for a video
Vimeo -> Vimeo : Generates SCORM package (internal process)
Vimeo --> User : Provides SCORM ZIP file for download

User -> LMS : Uploads SCORM ZIP file
LMS -> LMS : Processes and imports SCORM package (internal)

User -> LMS : Publishes course
LMS -> LMS : Makes Vimeo content available within course
LMS --> User : Course published; content accessible
@enduml

---

UML 3.
@startuml
title Learner Accessing Vimeo Content within LMS

actor "Learner" as Learner
participant "Learning Management System (LMS)" as LMS
database "LMS Gradebook" as LMSGradebook

box "Vimeo System" #LightBlue
  participant "Embedded Vimeo Content" as VimeoContent
  participant "Vimeo Playback Service" as VimeoPlayback
end box

Learner -> LMS : Logs in and accesses course with Vimeo video
LMS --> Learner : Displays course content with embedded Vimeo player
VimeoContent -> VimeoPlayback : Requests video stream and player features
VimeoPlayback --> VimeoContent : Streams video and provides player
Learner -> VimeoContent : Watches and interacts with video
VimeoPlayback -> LMSGradebook : Logs viewing activity and calculates score
Note over VimeoPlayback, LMSGradebook
Score is calculated based on configured settings (e.g., percentage watched, pass/fail).
Vimeo sends one score per attempt.
The LMS manages resubmission attempts.
End Note
LMSGradebook --> LMS : Sends calculated grade
LMS --> Learner : Displays completion/grade information
Learner -> LMS : Reviews score in LMS gradebook
LMS -> LMSGradebook : Requests gradebook data
LMSGradebook --> LMS : Provides grade information
LMS --> Learner : Displays gradebook
@enduml

---

UML 4.
@startuml
title SCORM/xAPI Integration Flow

actor User
actor Learner
participant "Learning Management System (LMS)" as LMS

box "Vimeo System" #LightBlue
  participant "Vimeo Server" as Vimeo_Server
  participant "Vimeo (SCORM/xAPI Package)" as Vimeo_Package
  participant "Vimeo Player" as Vimeo_Player
end box

User -> Vimeo_Server: Downloads ZIP file (SCORM/xAPI Package)
activate User
deactivate User
Vimeo_Server --> User: Provides Vimeo_Package (ZIP file)

User -> LMS: Uploads Vimeo_Package (ZIP file)
activate LMS
LMS -> LMS: Unpacks and interprets contents (instructions, metadata)
LMS -> LMS: Extracts secure link / embed code

Learner -> LMS: Logs in and accesses assignment/course
activate Learner
LMS -> Learner: Displays interface with Vimeo Player
deactivate LMS

Vimeo_Player -> Vimeo_Server: Requests video stream via secure link / embed code
activate Vimeo_Player
activate Vimeo_Server
Vimeo_Server --> Vimeo_Player: Streams video content
deactivate Vimeo_Server

Learner -> Vimeo_Player: Interacts with video (watches, pauses, etc.)
Vimeo_Player -->> LMS: Sends viewing activity & progress data (SCORM/xAPI communication)
activate LMS
LMS -> LMS: Records data, calculates grade/completion status
LMS --> Learner: Displays score in gradebook
deactivate LMS
deactivate Learner
deactivate Vimeo_Player
@enduml


