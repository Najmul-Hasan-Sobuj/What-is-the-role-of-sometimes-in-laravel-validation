

# What is the role of sometimes in laravel validation

```
  $validator = Validator::make(
        $request->all(),
        [
            'title'       => 'required|string',
            'image'       => 'sometimes|image|mimes:png,jpg,jpeg|max:10000',
            'description' => 'required|string',
        ],
        [
            'mimes' => 'The :attribute must be a file of type: png - jpeg - jpg'
        ],
    );

   if ($validator->passes()) {

        //your code

    } else {
        $messages = $validator->messages();
        foreach ($messages->all() as $message) {
            Toastr::error($message, 'Failed', ['timeOut' => 30000]);
        }
    }
    return redirect()->back();
```

In Laravel, the `Validator` class provides a convenient way to validate incoming HTTP request data. Here, `$validator = Validator::make()` creates a new validator instance based on the `$request->all()`, which contains all of the input data from the form submission or HTTP request.

The `sometimes` rule in the validation rules array is used when we want to apply a validation rule only if a given attribute is present in the input. For example, in this case, the `image` field may not always be present in the request, so we use the `sometimes` rule to include it only if it is present.

If the `image` field is present, it must meet the following additional criteria: 

- It must be an image file (as specified by the `image` rule)
- It must have one of the allowed file extensions: "png", "jpg", "jpeg" (as specified by the `mimes` rule)
- It must be no larger than 10000 kilobytes (as specified by the `max` rule)

Finally, the custom error message for the `mimes` rule is defined using the `=>` syntax as an associative array item in the third parameter of `Validator::make()`. This message will be displayed if the file uploaded is not of the specified MIME type(s).
