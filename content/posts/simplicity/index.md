+++
title = 'Simplicity'
date = 2025-11-18T17:20:00-08:00
categories = ['dev']
tags = ['programming']
author = 'Colin'
+++

It's rare that I find myself writing new code. Creating a new file with a new class or function happens of course, but most of the time I'm modifying something that already exists to add something new or change what is there. In these cases, it can be tempting to just jam in the new stuff into whatever already exists. This is most commonly what is done, but probably not what should be done.

In an Android app for example, you may be working on a [Fragment](https://developer.android.com/guide/fragments) where you need to add some additional logic into the `onCreateView` method.

```kotlin
override fun onCreateView(
  inflater : LayoutInflater,
  container : ViewGroup?,
  savedInstanceState : Bundle?
): View? {
  val view = inflater.inflate(R.layout.fragment_profile, container, false)

  nameTextView = view.findViewById(R.id.name_text_view)
  emailTextView = view.findViewById(R.id.email_text_view)
  saveButton = view.findViewById(R.id.save_button)

  nameTextView.text = "Jane Doe"
  emailTextView.text = "jane.doe@example.com"
  saveButton.setOnClickListener {
    var data = UserData.builder()
      .name(nameTextView.text)
      .email(emailTextView.text)
      .build()

    userDao.save(data)
    navigator.navigateToSaved()
  }

  return view
}
```

Let's say in the above example I want to add in a new item to my page to be saved and I also want to add in some code that will track usage metrics of each of the various elements, binding them to a system that tracks impressions and interactions. I could just inline add each of these features and slowly the `onCreateView` method gets larger and larger. However, if I stop and break down the existing method first, the codebase becomes more readable and easier to think about.

```kotlin
override fun onCreateView(
  inflater : LayoutInflater,
  container : ViewGroup?,
  savedInstanceState : Bundle?
): View? {
  val view = inflater.inflate(R.layout.fragment_profile, container, false)

  assignViews(view)
  initViews()
  saveButton.setOnClickListener{ onSaveButtonClick() }

  return view
}

fun assignViews(view : View) {
  nameTextView = view.findViewById(R.id.name_text_view)
  emailTextView = view.findViewById(R.id.email_text_view)
  saveButton = view.findViewById(R.id.save_button)
}

fun initViews() {
  nameTextView.text = "Jane Doe"
  emailTextView.text = "jane.doe@example.com"
}

fun onSaveButtonClick() {
  var data = UserData.builder()
      .name(nameTextView.text)
      .email(emailTextView.text)
      .build()

    userDao.save(data)
    navigator.navigateToSaved()
}
```

I've now split the various steps that are occurring in the onCreateView method into their own smaller methods. When reading onCreateView now, it's very straight forward. You can read it like english and each step makes sense. Adding additional logic can be done either in the sub-methods that are being called, or by adding in a new method that contains sets of code for new logic.

Ideally we want to keep our method sizes as small as possible while still performing something of value.

I find that most code that is overly large can be broken up in this way to make the code easier to read before adding in whatever functionality one needs to add. Sometimes this can be done at the method level as described above, and other times it may need to be done at the class level where we break down a full class into smaller components that work together rather than containing all of the logic in an overly large class.

In general, making code shorter and more pleasant to read will result in both better and more maintainable code, and more joy in writing and reading the code bases that you work in.
