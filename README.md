# Vimeo LMS Integration: SCORM & xAPI Guidance

As means of guidance on integrating Vimeo video content with Learning Management Systems (LMS) through SCORM and xAPI standards, this repository explains the practical steps for enterprise account holders to set up e-learning preferences, export SCORM packages, and enable learners to engage with Vimeo content within an LMS.

---

## Understanding the integration process

Integrating Vimeo content with an LMS via SCORM or xAPI involves specific packaging and communication methods, rather than direct display. The following sections detail the core procedures and interactions.

### The SCORM/xAPI integration package explained
The downloadable ZIP file from Vimeo acts as a complete integration package, adhering to either SCORM or xAPI e-learning standards. This package is specifically designed for use by an LMS, providing it with all the necessary instructions and information for seamless integration and tracking of the associated Vimeo content.

When you upload this ZIP file, the LMS unpacks and interprets its contents. This package gives the LMS the exact details and commands needed to correctly start and show the Vimeo video player within its own system. It is important to remember that the actual video content remains on Vimeo's dedicated servers. The SCORM/xAPI package within the ZIP file typically contains a secure link or embed code. When the LMS processes this, it instructs the system to display the Vimeo video player, which then streams the video directly from Vimeo.(Figure 4)

The LMS then creates an interface within the course module, often appearing as an embedded player or a clickable link that opens the video. This interface allows the learner to engage with the Vimeo video. Crucially, the SCORM/xAPI communication protocols built into the package enable a continuous exchange of data between the Vimeo player and the LMS. This two-way communication allows the LMS to accurately record and receive comprehensive data about the learner's viewing progress and completion status, which is then used for accurate grading and full performance tracking.


<p align="center">
  <img width="1212" height="670" alt="image" src="https://github.com/user-attachments/assets/d1498102-e275-497f-8b25-2d67a145c46a" />
  <br>
  Figure 4: The SCORM/xAPI integration flow (UML)
</p>

Let's look into the details.

### Setting up default LMS preferences

The initial configuration of general LMS preferences within your Vimeo account includes setting up learner management, choosing technical standards (SCORM 1.2, SCORM 2004 v3, xAPI, AICC, cmi5), selecting scoring methods (percentage watched, pass/fail), and defining completion percentage thresholds (Figure 1). Please note that Learner IDs, sent from the LMS to Vimeo via SCORM packages, are linked to Vimeo users, especially when Single Sign-On (SSO) is in use. 

<p align="center">
  <img width="734" height="709" alt="image" src="https://github.com/user-attachments/assets/df392ad8-5699-40b2-9b7e-81f8411d0647" />
  <br>
  Figure 1: Setting up default LMS preferences (UML)
</p>


### SCORM export and LMS integration
A Vimeo Export Service, which is a backend component, creates the SCORM ZIP file. The LMS handles the import and publishing of this package within its own system.(Figure 2)

<p align="center">
  <img width="1129" height="553" alt="image" src="https://github.com/user-attachments/assets/4758a5a9-b247-4e84-b041-2ddbf65f6085" />
  <br>
  Figure 2: SCORM export and LMS integration (UML)
</p>



### Learner accessing Vimeo content within the LMS
The embedded Vimeo content is the player displayed inside the LMS, while the Vimeo Playback Service manages video streaming and logging from Vimeo's servers (Figure 3). Scoring is determined by your chosen methods, and the LMS controls how many times a learner can resubmit.

<p align="center">
  <img width="1187" height="637" alt="image" src="https://github.com/user-attachments/assets/1d585ded-c354-44f6-8542-6b3578b78c94" />
  <br>
  Figure 3: Learner accessing Vimeo content within the LMS (UML)
</p>


### Further information
[Vimeo integration with LMS (SCORM and xAPI)](https://help.vimeo.com/hc/en-us/articles/34850919923089-Vimeo-integration-with-LMS-SCORM-and-xAPI)


