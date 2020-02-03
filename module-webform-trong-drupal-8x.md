# Module Webform trong Drupal 8x

## Giới thiệu về Webform

Webform is the module for making forms and surveys in Drupal. After a submission customizable e-mails can be sent to administrators and/or submitters. Results can be exported into Excel or other spreadsheet applications. Webform also provides some basic statistical review and has an extensive API for expanding its features.

## Installing the [Webform Module](https://www.drupal.org/project/webform)

Copy/upload the webform module to the modules directory of your Drupal installation.

* Enable the 'Webform' module and desired sub-modules in 'Extend'. \(/admin/modules\)
* Set up user permissions. \(/admin/people/permissions\#module-webform\)
* Build a new webform \(/admin/structure/webform\) or duplicate an existing template \(/admin/structure/webform/templates\).
* Publish your webform as a:
  * **Page:** By linking to the published webform. \(/webform/contact\)
  * **Node:** By creating a new node that references the webform. \(/node/add/webform\)
  * **Block:** By placing a Webform block on your site. \(/admin/structure/block\)
* \(optional\) Install third party libraries\(/admin/help/webform\).
* \(optional\) Install add-on contrib modules\]\(/admin/structure/webform/addons\).

## Webform Features

Webform module cho phép bạn có thể build bất cứ loại form nào mà có thể thu thập nhiều loại data, nơi mà có thể submit vào nhiều form hoặc hệ thống. Mỗi một behavior của form của bạn và dữ liệu đầu vào đều có thể customize được . Khi bạn cần một multi-page form chứa nhiều cột với điều kiện logic hoặc simple contact form có thể đẩy dữ liệu vào SalesForce/CRM thì bạn có thể sử dụng tất cả nó ở trong webform module dành cho Drupal 8.

Drupal và mô-đun Webform cố gắng truy cập đầy đủ cho tất cả người dùng và người xây dựng trang web. Các công nghệ hỗ trợ, bao gồm screen readers và keyboard access, được hỗ trợ đầy đủ.



### Form manager <a id="s-form-manager"></a>

| [![Form manager](https://www.drupal.org/files/webform-8.x.5.x-features--form-manager.png) **Form manager**](https://www.drupal.org/files/webform-8.x.5.x-features--form-manager.png) | [![ Add webform](https://www.drupal.org/files/webform-8.x.5.x-features--form-manager-add.png) **Add webform**](https://www.drupal.org/files/webform-8.x.5.x-features--form-manager-add.png) |
| :--- | :--- |


The form manager provides a list of all available webforms.

Form manager features include:

* Filtering by keyword, category, and status
* Sorting by total number of submissions
* Archiving of old forms

### Form builder <a id="s-form-builder"></a>

| [![Form builder](https://www.drupal.org/files/webform-8.x.5.x-features--form-builder.png) **Form builder**](https://www.drupal.org/files/webform-8.x.5.x-features--form-builder.png) | [![Edit element](https://www.drupal.org/files/webform-8.x.5.x-features--form-builder.png) **Edit element**](https://www.drupal.org/files/webform-8.x.5.x-features--form-builder.png) |
| :--- | :--- |


The Webform module provides an intuitive form builder based upon Drupal 8's best practices for user interface design and user experience. The form builder allows non-technical users to easily build and maintain webforms.

Form builder features include:

* Drag-n-drop form element management
* Multi-column layout management
* Conditional logic overview
* Element duplication

### Configuration settings <a id="s-configuration-settings"></a>

Form behaviors, features, submission handling, messaging, and confirmations are completely customizable using global settings and/or form-specific settings.

| [![ General](https://www.drupal.org/files/webform-8.x.5.x-features--settings-general.png) **General**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-general.png) | [![ Form](https://www.drupal.org/files/webform-8.x.5.x-features--settings-form.png) **Form**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-form.png) |
| :--- | :--- |


#### General settings <a id="s-general-settings"></a>

Allow a webform's administrative information, paths, behaviors, and third-party settings to be customized.

General settings include:

* Categorization
* Customizable paths
* Disable saving of results
* Ajax support

#### Form settings <a id="s-form-settings"></a>

Allow a form's status, attributes, behaviors, labels, messages, wizard settings, and preview to be customized.

Form settings include:

* Open and close date/time scheduling
* Login redirection with custom messaging.
* Multiple step wizard forms
* Submission preview
* Input prepopulation using query string parameters.

| [![ Submisssions](https://www.drupal.org/files/webform-8.x.5.x-features--settings-submissions.png) **Submisssions**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-submissions.png) | [![ Confirmation](https://www.drupal.org/files/webform-8.x.5.x-features--settings-confirmation.png) **Confirmation**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-confirmation.png) |
| :--- | :--- |


#### Submissions settings <a id="s-submissions-settings"></a>

Allows a submission's labels, behaviors, limits, and draft settings to be customized.

Submission settings include:

* Saving of drafts
* Automatic purging of submissions
* Submission limits per user and/or per form
* Autofilling form using previously submitted values

#### Confirmation settings <a id="s-confirmation-settings"></a>

Allows the form's confirmation type, message, and URL to be customized.

Confirmation types include:

* Dedicated page
* Redirect to internal or external URL
* Displaying of a custom status message
* Opening a modal dialog

| [![ Handlers](https://www.drupal.org/files/webform-8.x.5.x-features--settings-handlers.png) **Handlers**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-handlers.png) | [![ Email handler](https://www.drupal.org/files/webform-8.x.5.x-features--settings-handlers-email.png) **Email handler**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-handlers-email.png) |
| :--- | :--- |


#### Emails / Handlers <a id="s-emails-handlers"></a>

Allows additional actions and behaviors to be processed when a webform or submission is created, updated, or deleted. Handlers are used to route submitted data to external applications and send notifications & confirmations.

Email support features include:

* Previewing and resending emails
* Sending HTML emails
* File attachments \(requires the Mail System and Swift Mailer module.\)
* HTML and plain-text email-friendly Twig templates
* Customizable display formats for individual form elements

Remote post features include: - Posting selected elements to a remote server - Adding custom parameters to remote post requests

| [![ CSS/JS assets](https://www.drupal.org/files/webform-8.x.5.x-features--settings-assets.png) **CSS/JS assets**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-assets.png) | [![ Access](https://www.drupal.org/files/webform-8.x.5.x-features--settings-access.png) **Access**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-access.png) |
| :--- | :--- |


#### CSS/JS assets <a id="s-cssjs-assets"></a>

The CSS/JS assets page allows site builders to attach custom CSS and JavaScript to a webform. Custom CSS can be used to make simple layout or design tweaks to a form. Custom JavaScript allows additional conditional logic and behaviors to be added to a form.

#### Access settings <a id="s-access-settings"></a>

Allows an administrator to determine who can administer a webform and/or create, update, delete, and purge webform submissions.

### Elements <a id="s-elements"></a>

| [![Elements](https://www.drupal.org/files/webform-8.x.5.x-features--elements.png) **Elements**](https://www.drupal.org/files/webform-8.x.5.x-features--elements.png) | [![Element settings](https://www.drupal.org/files/webform-8.x.5.x-features--elements-settings.png) **Element settings**](https://www.drupal.org/files/webform-8.x.5.x-features--elements-settings.png) |
| :--- | :--- |


The Webform module is built directly on top of Drupal 8's Form API. Every form element available in Drupal 8 is supported by the Webform module.

Form elements include:

* **Basic HTML**: Textfield, Textareas, Checkboxes, Radios, Select menu, Password, and more...
* **Advanced HTML5**: Email, Url, Number, Telephone, Date, Number, Range, and more...
* **Advanced Drupal**: File uploads, Entity References, Table select, Date list, and more...
* **Widgets**: Likert scale, Star rating, Buttons, Geolocation, Terms of service, Select/Checkboxes/Radios with other, and more...
* **Markup**: Dismissible messages, Basic HTML, Advanced HTML, Details, and Fieldsets.
* **Composites**: Name, Address, Contact, Credit Card, and event custom composites
* **Computed**: Calculated values using Tokens and Twig with Ajax support.

#### Element settings <a id="s-element-settings"></a>

All of Drupal 8's default form element properties and behaviors are supported. There are also several custom webform element properties and settings available to enhance a form element's behavior.

Standard and custom properties allow for:

* Customizable error validation messages
* Conditional logic using [FAPI States API](https://api.drupal.org/api/examples/form_example%21form_example_states.inc/function/form_example_states_form/7)
* Input masks \(using [jquery.inputmask](https://github.com/RobinHerbots/jquery.inputmask)\)
* [Select2](https://select2.github.io/) or [Chosen](https://harvesthq.github.io/chosen/) replacement of select boxes
* Word and character counting for text elements
* Help tooltips \(using [jQuery UI Tooltip](https://jqueryui.com/tooltip/)\)
* More information slideouts
* Regular expression pattern validation
* Private elements, visible only to administrators
* Unique values per element

| [![Conditional logic](https://www.drupal.org/files/webform-8.x.5.x-features--elements-conditional.png) **Conditional logic**](https://www.drupal.org/files/webform-8.x.5.x-features--elements-conditional.png) | [![View source](https://www.drupal.org/files/webform-8.x.5.x-features--elements-source.png) **View source**](https://www.drupal.org/files/webform-8.x.5.x-features--elements-source.png) |
| :--- | :--- |


#### States/Conditional logic <a id="s-statesconditional-logic"></a>

Drupal's State API can be used by developers to provide conditional logic to hide and show form elements.

Drupal's State API supports:

* Show/Hide
* Required/Optional
* Open/Close
* Enable/Disable

#### Viewing source <a id="s-viewing-source"></a>

At the heart of a Webform module's form elements is a Drupal [render array](https://www.drupal.org/docs/8/api/render-api/render-arrays), which can be edited and managed by developers. The Drupal render array gives developers complete control over a webform's elements, layout, and look-and-feel by allowing developers to make bulk updates to a webform's label, descriptions, and behaviors.

### Forms <a id="s-forms"></a>

| [![Accessibility](https://www.drupal.org/files/webform-8.x.5.x-features--forms-accessiblity.png) **Accessibility**](https://www.drupal.org/files/webform-8.x.5.x-features--forms-accessiblity.png) | [![Multistep form](https://www.drupal.org/files/webform-8.x.5.x-features--forms-wizard.png) **Multistep form**](https://www.drupal.org/files/webform-8.x.5.x-features--forms-wizard.png) |
| :--- | :--- |


#### Accessibility <a id="s-accessibility"></a>

The outputted forms and even the Webform module's administrative interface \(i.e. form builder\) are accessible using keyboard navigation and screen readers. The Webform module complies with [WCAG 2.0](http://www.w3.org/TR/WCAG20/#contents) and [ATAG 2.0](http://www.w3.org/TR/ATAG20/#contents) guidelines.

#### Multistep form <a id="s-multistep-form"></a>

Forms can be broken up into multiple pages using a progress bar. Authenticated users can save drafts and/or have their changes automatically saved as they progress through a long form.

Multistep form features include:

* Customizable progress bar
* Customizable previous and next button labels and styles
* Saving drafts between steps

#### Drupal integration​ <a id="s-drupal-integration"></a>

| [![Block](https://www.drupal.org/files/webform-8.x.5.x-features--forms-block.png) **Block**](https://www.drupal.org/files/webform-8.x.5.x-features--forms-block.png) | [![Node](https://www.drupal.org/files/webform-8.x.5.x-features--forms-node.png) **Node**](https://www.drupal.org/files/webform-8.x.5.x-features--forms-node.png) |
| :--- | :--- |


Webforms can be attached to nodes or displayed as blocks. Webforms can also have dedicated SEO-friendly URLs. Form elements are render arrays that can easily be altered using custom hooks and/or plugins.

### Results management <a id="s-results-management"></a>

| [![Results](https://www.drupal.org/files/webform-8.x.5.x-features--results.png) **Results**](https://www.drupal.org/files/webform-8.x.5.x-features--results.png) | [![Customize results](https://www.drupal.org/files/webform-8.x.5.x-features--results-customize.png) **Customize results**](https://www.drupal.org/files/webform-8.x.5.x-features--results-customize.png) |
| :--- | :--- |


Form submissions can optionally be stored in the database, reviewed, and downloaded. Submissions can also be flagged with administrative notes.

Results management features include:

* Submission flagging, locking, and notes
* Viewing submissions as HTML, plain text, and YAML
* Customizable reports
* Downloading results as a CSV to Google Sheets or MS Excel
* Saving of download preferences per form
* [Drupal Views](https://www.drupal.org/docs/8/core/modules/views) integration for advanced reporting.

### Access controls <a id="s-access-controls"></a>

| [![Permissions](https://www.drupal.org/files/webform-8.x.5.x-features--access-permissions.png) **Permissions**](https://www.drupal.org/files/webform-8.x.5.x-features--access-permissions.png) | [![Element access](https://www.drupal.org/files/webform-8.x.5.x-features--access-element.png) **Element access**](https://www.drupal.org/files/webform-8.x.5.x-features--access-element.png) |
| :--- | :--- |


The Webform module provides full access controls and permissions for managing who can create forms, post submissions, and access a webform's results. Access controls can be applied to roles and/or specific users. The Webform access submodule allows you to even setup reusable permission groups which can be applied to multiple instances of the same webform.

Access controls allow users to:

* Create new forms
* Update forms
* Delete forms
* View submissions
* Update submissions
* Delete submissions
* View selected elements
* Update selected elements

### Reusable templates <a id="s-reusable-templates"></a>

| [![Templates](https://www.drupal.org/files/webform-8.x.5.x-features--templates.png) **Templates**](https://www.drupal.org/files/webform-8.x.5.x-features--templates.png) | [![Templates preview](https://www.drupal.org/files/webform-8.x.5.x-features--templates-preview.png) **Templates preview**](https://www.drupal.org/files/webform-8.x.5.x-features--templates-preview.png) |
| :--- | :--- |


The Webform module provides a few starter templates and multiple example forms which webform administrators can update or use to create new reusable templates for their organization.

Starter templates include:

* Contact Us
* Donation
* Employee Evaluation
* Issue
* Job Application
* Job Seeker Profile
* Registration
* Session Evaluation
* Subscribe
* User Profile

### Reusable options <a id="s-reusable-options"></a>

| [![Options](https://www.drupal.org/files/webform-8.x.5.x-features--options.png) **Options**](https://www.drupal.org/files/webform-8.x.5.x-features--options.png) | [![Likert](https://www.drupal.org/files/webform-8.x.5.x-features--options-likert.png) **Likert**](https://www.drupal.org/files/webform-8.x.5.x-features--options-likert.png) |
| :--- | :--- |


Administrators can define reusable global options for select menus, checkboxes, and radio buttons. The Webform module includes default options for states, countries, demographics, likert answers, and more.

Reusable options include:

* **Geographic**: Languages, country, and states
* **Date and time**: Days, months, and time zones
* **Demographic**: Education, employment status, ethnicity, Industry, languages, marital status, relationship, size, and job titles
* **Likert**: Agreement, comparison, importance, quality, satisfaction, ten scale, and would you

### Internationalization <a id="s-internationalization"></a>

Forms and configuration can be translated into multiple languages using Drupal's \[configuration translation system\]\([https://www.drupal.org/docs/8/core/modules/config-translation](https://www.drupal.org/docs/8/core/modules/config-translation).

### Add-ons <a id="s-add-ons"></a>

| [![Add-ons](https://www.drupal.org/files/webform-8.x.5.x-features--addons.png) **Add-ons**](https://www.drupal.org/files/webform-8.x.5.x-features--addons.png) | [![Analysis](https://www.drupal.org/files/webform-8.x.5.x-features--addons-webform-analysis.png) **Analysis**](https://www.drupal.org/files/webform-8.x.5.x-features--addons-webform-analysis.png) |
| :--- | :--- |


There are [dozens of add-ons available](https://www.drupal.org/node/2837065) that extend and/or provide additional functionality to the Webform module and Drupal's Form API.

Add-ons include:

* Analysis for creating graphs and charts
* CRM integration including SalesForce, HubSpot, MyEmma, SugarCRM, more…
* SPAM protection
* Advanced workflows
* Data encryption
* GDPR compliance

### Development tools <a id="s-development-tools"></a>

| [![Test](https://www.drupal.org/files/webform-8.x.5.x-features--devel-test.png) **Test**](https://www.drupal.org/files/webform-8.x.5.x-features--devel-test.png) | [![API](https://www.drupal.org/files/webform-8.x.5.x-features--devel-api.png) **API**](https://www.drupal.org/files/webform-8.x.5.x-features--devel-api.png) |
| :--- | :--- |


Examples and tools are provided to help developers get started customizing existing features and adding new features to the Webform module.

Development tools include:

* Test forms using customizable default values
* Easy to export configuration files
* Debugging tools for all handlers
* Examples for external API integration using remotes posts or custom code
* Example modules for creating custom elements and handlers
* Demos for building event registration and application evaluation system

### Drush & Composer integration <a id="s-drush-composer-integration"></a>

| [![Drush](https://www.drupal.org/files/webform-8.x.5.x-features--drush.png) **Drush**](https://www.drupal.org/files/webform-8.x.5.x-features--drush.png) | [![Composer](https://www.drupal.org/files/webform-8.x.5.x-features--drush-composer.png) **Composer**](https://www.drupal.org/files/webform-8.x.5.x-features--drush-composer.png) |
| :--- | :--- |


Drush commands are provided to:

* Generate multiple submissions
* Export submissions
* Purge submissions
* Download and manage third-party libraries
* Generate a composer.js file for third-party libraries
* Tidy YAML configuration files







