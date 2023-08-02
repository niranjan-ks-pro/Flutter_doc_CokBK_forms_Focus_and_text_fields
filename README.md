# Flutter_doc_CokBK_forms_Focus_and_text_fields
 https://docs.flutter.dev/cookbook/forms/focus
Create and style a text field

=============================

1\.  [Cookbook](https://docs.flutter.dev/cookbook)

2\.  [Forms](https://docs.flutter.dev/cookbook/forms)

3\.  [Create and style a text field](https://docs.flutter.dev/cookbook/forms/text-input)

Text fields allow users to type text into an app. They are used to build forms, send messages, create search experiences, and more. In this recipe, explore how to create and style text fields.

Flutter provides two text fields: [`TextField`](https://api.flutter.dev/flutter/material/TextField-class.html) and [`TextFormField`](https://api.flutter.dev/flutter/material/TextFormField-class.html).

[](https://docs.flutter.dev/cookbook/forms/text-input#textfield)`TextField`

---------------------------------------------------------------------------

[`TextField`](https://api.flutter.dev/flutter/material/TextField-class.html) is the most commonly used text input widget.

By default, a `TextField` is decorated with an underline. You can add a label, icon, inline hint text, and error text by supplying an [`InputDecoration`](https://api.flutter.dev/flutter/material/InputDecoration-class.html) as the [`decoration`](https://api.flutter.dev/flutter/material/TextField/decoration.html) property of the `TextField`. To remove the decoration entirely (including the underline and the space reserved for the label), set the `decoration` to null.

content_copy

```

TextField(

  decoration: InputDecoration(

    border: OutlineInputBorder(),

    hintText: 'Enter a search term',

  ),

),

```

To retrieve the value when it changes, see the [Handle changes to a text field](https://docs.flutter.dev/cookbook/forms/text-field-changes/) recipe.

[](https://docs.flutter.dev/cookbook/forms/text-input#textformfield)`TextFormField`

-----------------------------------------------------------------------------------

[`TextFormField`](https://api.flutter.dev/flutter/material/TextFormField-class.html) wraps a `TextField` and integrates it with the enclosing [`Form`](https://api.flutter.dev/flutter/widgets/Form-class.html). This provides additional functionality, such as validation and integration with other [`FormField`](https://api.flutter.dev/flutter/widgets/FormField-class.html) widgets.

content_copy

```

TextFormField(

  decoration: const InputDecoration(

    border: UnderlineInputBorder(),

    labelText: 'Enter your username',

  ),

),

```

`

`Focus and text fields
=====================

1.  [Cookbook](https://docs.flutter.dev/cookbook)
2.  [Forms](https://docs.flutter.dev/cookbook/forms)
3.  [Focus and text fields](https://docs.flutter.dev/cookbook/forms/focus)

When a text field is selected and accepting input, it is said to have "focus." Generally, users shift focus to a text field by tapping, and developers shift focus to a text field programmatically by using the tools described in this recipe.

Managing focus is a fundamental tool for creating forms with an intuitive flow. For example, say you have a search screen with a text field. When the user navigates to the search screen, you can set the focus to the text field for the search term. This allows the user to start typing as soon as the screen is visible, without needing to manually tap the text field.

In this recipe, learn how to give the focus to a text field as soon as it's visible, as well as how to give focus to a text field when a button is tapped.

[](https://docs.flutter.dev/cookbook/forms/focus#focus-a-text-field-as-soon-as-its-visible)Focus a text field as soon as it's visible
-------------------------------------------------------------------------------------------------------------------------------------

To give focus to a text field as soon as it's visible, use the `autofocus` property.

content_copy

```
TextField(
  autofocus: true,
);

```

For more information on handling input and creating text fields, see the [Forms](https://docs.flutter.dev/cookbook#forms) section of the cookbook.

[](https://docs.flutter.dev/cookbook/forms/focus#focus-a-text-field-when-a-button-is-tapped)Focus a text field when a button is tapped
--------------------------------------------------------------------------------------------------------------------------------------

Rather than immediately shifting focus to a specific text field, you might need to give focus to a text field at a later point in time. In the real world, you might also need to give focus to a specific text field in response to an API call or a validation error. In this example, give focus to a text field after the user presses a button using the following steps:

1.  Create a `FocusNode`.
2.  Pass the `FocusNode` to a `TextField`.
3.  Give focus to the `TextField` when a button is tapped.

### [](https://docs.flutter.dev/cookbook/forms/focus#1-create-a-focusnode)1\. Create a `FocusNode`

First, create a [`FocusNode`](https://api.flutter.dev/flutter/widgets/FocusNode-class.html). Use the `FocusNode` to identify a specific `TextField` in Flutter's "focus tree." This allows you to give focus to the `TextField` in the next steps.

Since focus nodes are long-lived objects, manage the lifecycle using a `State` object. Use the following instructions to create a `FocusNode` instance inside the `initState()` method of a `State` class, and clean it up in the `dispose()` method:

content_copy

```
// Define a custom Form widget.
class MyCustomForm extends StatefulWidget {
  const MyCustomForm({super.key});

  @override
  State<MyCustomForm> createState() => _MyCustomFormState();
}

// Define a corresponding State class.
// This class holds data related to the form.
class _MyCustomFormState extends State<MyCustomForm> {
  // Define the focus node. To manage the lifecycle, create the FocusNode in
  // the initState method, and clean it up in the dispose method.
  late FocusNode myFocusNode;

  @override
  void initState() {
    super.initState();

    myFocusNode = FocusNode();
  }

  @override
  void dispose() {
    // Clean up the focus node when the Form is disposed.
    myFocusNode.dispose();

    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    // Fill this out in the next step.
  }
}
```

### [](https://docs.flutter.dev/cookbook/forms/focus#2-pass-the-focusnode-to-a-textfield)2\. Pass the `FocusNode` to a `TextField`

Now that you have a `FocusNode`, pass it to a specific `TextField` in the `build()` method.

content_copy

```
@override
Widget build(BuildContext context) {
  return TextField(
    focusNode: myFocusNode,
  );
}
```

### [](https://docs.flutter.dev/cookbook/forms/focus#3-give-focus-to-the-textfield-when-a-button-is-tapped)3\. Give focus to the `TextField` when a button is tapped

Finally, focus the text field when the user taps a floating action button. Use the [`requestFocus()`](https://api.flutter.dev/flutter/widgets/FocusNode/requestFocus.html) method to perform this task.

content_copy

```
FloatingActionButton(
  // When the button is pressed,
  // give focus to the text field using myFocusNode.
  onPressed: () => myFocusNode.requestFocus(),
),
```
