# Drupal Ajax Form

## Overview

Thêm event ajax callback vào trường của form để có thể update fields hoặc thêm markup, để người dùng có thể tương tác với form.

#### Ajax callback function có thể sử dụng để :

* Có thể update hoặc thêm mới fields của form
* Update giá trị của fields
* Chạy các hàm tiền xử lý ajax hặc có thể chạy code Javascript

Nếu bạn muốn tạo các ràng buộc fields, ẩn hiện dựa vào fields khác , bạn có thể tham khảo   [Form API \#states property](https://www.drupal.org/docs/8/api/form-api/conditional-form-fields).

#### Các bước để sử dụng Ajax trong form của Drupal



1. Tạo ra một form mới hoặc sử dụng hàm [hook\_form\_alter](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Form%21form.api.php/function/hook_form_alter) để thay đổi một form có sẵn 
2. Thêm '\#ajax' khi render element của field sẽ dùng trong hàm callback
3. Thực hiện đặt tên của hàm callback và loại event sẽ thực hiện.
4. Khi mà sự kiện thay đổi giá trị của fields form,hàm callback sẽ được gọi.
5. Hàm allback sẽ cho phép truy cập $form array và  FormstateInterface và cuối cùng phải returm array hoặc html markup hoặc dùng [AJAX Command](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Ajax%21CommandInterface.php/interface/implements/CommandInterface).

## Ví dụ với Drupal Ajax Form

Bạn có thể sử dụng ajax event trong form của bạn hoặc attack custom event using [hook\_form\_alter](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Form%21form.api.php/function/hook_form_alter/8.7.x) 



```text
<?php

namespace Drupal\ajaxfilters\Form;

use Drupal\Core\Form\FormBase;
use Drupal\Core\Form\FormStateInterface;
use Drupal\Core\Ajax\AjaxResponse;
use Drupal\Core\Ajax\ReplaceCommand;

/**
 * Provides a default form.
 */
class DefaultForm extends FormBase {

  /**
   * {@inheritdoc}
   */
  public function getFormId() {
    return 'default_form';
  }

  /**
   * {@inheritdoc}
   */
  public function buildForm(array $form, FormStateInterface $form_state) {
    // Create a select field that will update the contents
    // of the textbox below.
    $form['example_select'] = [
      '#type' => 'select',
      '#title' => $this->t('Select element'),
      '#options' => [
        '1' => $this->t('One'),
        '2' => $this->t('Two'),
        '3' => $this->t('Three'),
        '4' => $this->t('From New York to Ger-ma-ny!'),
      ],
    ];

    // Create a textbox that will be updated
    // when the user selects an item from the select box above.
    $form['output'] = [
      '#type' => 'textfield',
      '#size' => '60',
      '#disabled' => TRUE,
      '#value' => 'Hello, Drupal!!1',      
      '#prefix' => '<div id="edit-output">',
      '#suffix' => '</div>',
    ];

    // Create the submit button.
    $form['submit'] = [
      '#type' => 'submit',
      '#value' => $this->t('Submit'),
    ];

    return $form;
  }

  /**
   * {@inheritdoc}
   */
  public function validateForm(array &$form, FormStateInterface $form_state) {
    parent::validateForm($form, $form_state);
  }

  /**
   * {@inheritdoc}
   */
  public function submitForm(array &$form, FormStateInterface $form_state) {
    // Display result.
    foreach ($form_state->getValues() as $key => $value) {
      \Drupal::messenger()->addStatus($key . ': ' . $value);
    }
  }

}
```

Drupal sẽ tự động sinh ra một ID cho tất cả các form elements và bạn có thể thấy output được render ra .Tuy nhiên để ngăn chặn việc ID có thể bị thay đổi , \#attributes' sẽ được sử dụng cho ID HTML cụ thể 



### Thêm AJAX event <a id="s-adding-the-ajax-event"></a>

Để có thể attack Ajax callback , bạn có thể thêm tag  '\#ajax'. Nó sẽ định nghĩa hàm , có thể truyền nhiều tham số khác nhau . Có thể tham khảo phần [Ajax API](https://api.drupal.org/api/drupal/core%21core.api.php/group/ajax) để có thểm xem thêm phần render các elements.

Thêm một ajax callback cho selected field, kết quả sẽ show ở textbox 

```text
// Create a select field that will update the contents
// of the textbox below.
$form['example_select'] = [
  '#type' => 'select',
  '#title' => $this->t('Example select field'),
  '#options' => [
    '1' => $this->t('One'),
    '2' => $this->t('Two'),
    '3' => $this->t('Three'),
    '4' => $this->t('From New York to Ger-ma-ny!'),
  ],
  '#ajax' => [
    'callback' => '::myAjaxCallback', // don't forget :: when calling a class method.
    //'callback' => [$this, 'myAjaxCallback'], //alternative notation
    'disable-refocus' => FALSE, // Or TRUE to prevent re-focusing on the triggering element.
    'event' => 'change',
    'wrapper' => 'edit-output', // This element is updated with this AJAX callback.
    'progress' => [
      'type' => 'throbber',
      'message' => $this->t('Verifying entry...'),
    ],
  ]
];
```

 Đó là thêm một Ajax event để có thể gọi đến method khi mình bấm vào chọn các option ở selection box.

**Explanation of the \#ajax tags used above:**

* **callback** =&gt; Hàm hoặc class method sẽ gọi thông qua AJAX request. Nếu bạn tạo forrm của bạn thì bạn có thể sử dụng class method như một callback và sẽ như sau : `'callback' => '::myAjaxCallback'` or `'callback' => [$this, 'myAjaxCallback']`. Nhưng nếu bạn sử dụng But if you instead used **hook\_form\_alter**\(..\)  để thay đổi một form có sẵn  thì bạn phải truyền thông qua  .module file như sau :`'callback' => 'myAjaxCallback'`.  
* **event** =&gt; The event to trigger on; any valid DOM event for the element can be used, simply omit the 'on' portion of the event. 'onclick' =&gt; 'click', 'onkeyup' =&gt; 'keyup', 'onchange' =&gt; 'change', etc.  
* **wrapper** =&gt; The id of the element you wish to change. If your callback returns a render array or markup, the wrapper with this id is replaced with your result.   
* **progress** =&gt; The indicator to use during the request so the user knows the page is waiting on a response from the server

A [full list of allowed properties](https://www.drupal.org/docs/8/api/ajax-api/basic-concepts#sub_form) can be found in the [Ajax API Basic Concepts Guide](https://www.drupal.org/docs/8/api/ajax-api/basic-concepts).

The wrapper element is optional and useful only when returning HTML in the next step. This ID should match the ID on the HTML/Form element you want to act upon. In the above example, the 'output' input element was given an ID of 'edit-ouput' and so 'wrapper' reflects that same ID.

_Note: The wrapper does not contain a hashtag prefix \(\#edit-output\) as you would use in CSS._ 

If you run this code now, you'll already see a Throbber icon appear when you select a value in the example select field, but you will find an error message in your Javascript console: 

```text
The website encountered an unexpected error. Please try again later.Symfony\Component\HttpKernel\Exception\HttpException: The specified #ajax callback is empty or not callable. in Drupal\Core\Form\FormAjaxResponseBuilder->buildResponse() (line 67 of core/lib/Drupal/Core/Form/FormAjaxResponseBuilder.php)
```

This happens because we haven't implemented our callback function yet.

### Implement the callback function <a id="s-implement-the-callback-function"></a>

Let's finally add the callback function that dynamically updates our form's textfield.

There are different ways to respond to the ajax request, depending on what you want to do in your AJAX callback.

* [**Render array** ](https://www.drupal.org/docs/8/api/javascript-api/ajax-forms#ajax_callback_render_array)=&gt; If you just want to update a field on your form you can simply return a render array, ie. $form\['field\_yourfieldname'\]. The resulting markup will be placed in the wrapper element, that was defined when attaching the \['\#ajax'\] render array to the form field.  
* [**Custom HTML markup** ](https://www.drupal.org/docs/8/api/javascript-api/ajax-forms#ajax_callback_html_markup)=&gt; If you want to display some information on your form that is not related to a field on your form, you can return HTML Markup that will be placed in the wrapper element, that was defined when attaching the \['\#ajax'\] render array to the form field. Basically you also return a render array because you have to wrap your HTML markup in a render array return `['#markup' => '<h1>Hello</h1>'];`.  
* [**AJAX Command**](https://www.drupal.org/docs/8/api/javascript-api/ajax-forms#ajax_callback_ajax_commands) =&gt; If you don't want to update your form at all but instead invoke an [AJAX Command,](http://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Ajax%21CommandInterface.php/interface/implements/CommandInterface) you have to return an AjaxResponse object. ****

#### Render Array <a id="s-render-array"></a>

First we'll fetch the selected value of the select field from the $form\_state interface and save it to the output textfield. Then we return a render array of the prepared textfield. This replaces the original textfield on the form. 

![Dynamic Drupal AJAX Forms](https://www.drupal.org/files/ajaxforms1.gif)

```text
// Get the value from example select field and fill
// the textbox with the selected text.
public function myAjaxCallback(array &$form, FormStateInterface $form_state) {
  // Prepare our textfield. check if the example select field has a selected option.
  if ($selectedValue = $form_state->getValue('example_select')) {
      // Get the text of the selected option.
      $selectedText = $form['example_select']['#options'][$selectedValue];
      // Place the text of the selected option in our textfield.
      $form['output']['#value'] = $selectedText;
  }
  // Return the prepared textfield.
  return $form['output']; 
}
```

The returned array _replaces_ the element with the ID specified by the wrapper element \(\#edit-output\). This is important to remember when deciding what to return from the callback! Whatever was specified by the given ID is completely replaced by the new HTML! Make sure that the returned field also contains the id \#edit-output or the next AJAX callback will not find a target to place the rendered code into.

#### HTML Markup <a id="s-html-markup"></a>

If you don't want to update the value of a form field but instead show some custom HTML markup on your form, you can also return HTML markup instead of a render array. Even though you can return raw HTML the return value must still be wrapped in a render array. Use `['#markup' => '<p>your markup</p>'` to return the response.

The returned markup entirely replaces the object with the id passed as **wrapper** in the \#ajax render array, attached to the form field, so don't forget to add the id, that you specified as wrapper in the \['\#ajax'\] render array in the custom markup you are returning from your callback.

The example below will replace the output textfield that was originally placed on our form with a DIV element that holds the selected text.

![](https://www.drupal.org/files/ajaxforms2.gif)

```text
// Get the value from example select field and fill
// the textbox with the selected text.
public function myAjaxCallback(array &$form, FormStateInterface $form_state) {
  $markup = 'nothing selected';

  // Prepare our textfield. Check if the example select field has a selected option.
  if ($selectedValue = $form_state->getValue('example_select')) {
      // Get the text of the selected option.
      $selectedText = $form['example_select']['#options'][$selectedValue];
      // Place the text of the selected option in our textfield.
      $markup = "<h1>$selectedText</h1>";
  }

  // Don't forget to wrap your markup in a div with the #edit-output id
  // or the callback won't be able to find this target when it's called
  // more than once.
  $output = "<div id='edit-output'>$markup</div>";

  // Return the HTML markup we built above in a render array.
  return ['#markup' => $output];
}
```

#### AJAX Commands \(AjaxResponse\) <a id="s-ajax-commands-ajaxresponse"></a>

You can also choose to return an AjaxResponse that issues AJAX commands via the client-side jQuery library when your callback function is executed. You can choose from a range of existing AJAX commands, implement a custom AJAX command or just run some Javascript code in one of your scripts.

The example callback function below will create a new textbox with the selected text and replace our original output textbox with it. Then it will show a modal dialogbox with the selected text from our select form element.

![Drupal AJAX Forms, Figure 4](https://www.drupal.org/files/ajaxforms3.gif)

```text
// Dont't forget to add the required namespaces at the beginning of your class/module.
use Drupal\Core\Ajax\AjaxResponse;
use Drupal\Core\Ajax\ReplaceCommand;
use Drupal\Core\Ajax\OpenModalDialogCommand;

/**
 * An Ajax callback.
 */
public function myAjaxCallback(array &$form, FormStateInterface $form_state) {
  // Try to get the selected text from the select element on our form.
  $selectedText = 'nothing selected';
  if ($selectedValue = $form_state->getValue('example_select')) {
    // Get the text of the selected option.
    $selectedText = $form['example_select']['#options'][$selectedValue];
  }

  // Create a new textfield element containing the selected text.
  // We're replacing the original textfield using an AJAX replace command which
  // expects HTML markup. So we need to render the textfield render array here.
  $elem = [
    '#type' => 'textfield',
    '#size' => '60',
    '#disabled' => TRUE,
    '#value' => "I am a new textfield: $selectedText!",
    '#attributes' => [
      'id' => ['edit-output'],
    ],
  ];
  $renderer = \Drupal::service('renderer');
  $renderedField = $renderer->render($elem);

  // Attach the javascript library for the dialog box command
  // in the same way you would attach your custom JS scripts.
  $dialogText['#attached']['library'][] = 'core/drupal.dialog.ajax';
  // Prepare the text for our dialogbox.
  $dialogText['#markup'] = "You selected: $selectedText";

  // If we want to execute AJAX commands our callback needs to return
  // an AjaxResponse object. let's create it and add our commands.
  $response = new AjaxResponse();
  // Issue a command that replaces the element #edit-output
  // with the rendered markup of the field created above.
  $response->addCommand(new ReplaceCommand('#edit-output', $renderedField));
  // Show the dialog box.
  $response->addCommand(new OpenModalDialogCommand('My title', $dialogText, ['width' => '300']));

  // Finally return the AjaxResponse object.
  return $response;
}
```

Như ở trong ví dụ trước , render array sẽ được tạo ra để thay thế element trước bằng việc thông qua ID vaò trong hàm  ReplaceCommand\(\).Trong trường hợp này the hashtag cũng cần phải có để nhận diện được element sẽ được thay thế . Sau đó popup sẽ được hiển thị 

Bạn có thể tìm thấy  [list of all commands](http://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Ajax%21CommandInterface.php/interface/implements/CommandInterface)  có thể dùng trong response  **`ở`** ~~.~~

### Execute code custom Javascript  AJAX callback <a id="s-execute-custom-javascript-in-an-ajax-callback"></a>

Bạn có thể viết custom Ajax comand nhưng bạn phải sử dụng javascript code.  [AJAX InvokeCommand](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Ajax%21InvokeCommand.php/class/InvokeCommand) có thể sử dụng để gọi Jquery.

Hàm xử lý ajax 

```text
use Drupal\Core\Form\FormStateInterface;
use Drupal\Core\Ajax\AjaxResponse;
use Drupal\Core\Ajax\InvokeCommand;

/**
 * An Ajax callback.
 */
public function myAjaxCallback(array &$form, FormStateInterface $form_state) {
  $response = new AjaxResponse();
  $response->addCommand(new InvokeCommand(NULL, 'myAjaxCallback', ['This is the new text!']));
  return $response;
}
```

Code Javascript:

```text
(function($) {
  // Argument passed from InvokeCommand.
  $.fn.myAjaxCallback = function(argument) {
    console.log('myAjaxCallback is called.');
    // Set textfield's value to the passed arguments.
    $('input#edit-output').attr('value', argument);
  };
})(jQuery);
```





####  

