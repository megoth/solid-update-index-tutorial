# How to update your front page in a Solid POD and signal that it shouldn't be overwritten by your POD provider - short version

This tutorial is a short version of [the full tutorial](./README.md).

## Get cookie value

Log in with your WebID and get ahold of the cookie-value for `connect.sid`. This value will be referred to as `<your-cookie-value>` going forward.

## (Optional) Download your current front page

If you want to build upon the existing index.html file, run the following command:

```
curl --cookie "connect.sid=<your-cookie-value>" https://<your-pod>/index.html > index.html
```

`<your-pod>` refers to your POD on your local POD provider, e.g. `megoth.solid.community`.

You now have a local copy of your front page.

## Add/change value for solid-allow-automatic-updates

Now you can edit `index.html` as much as you want. If you want to make sure that your POD provider do not overwrite it at a later point, you need to add the following in the `head`-tag:

```
<meta name="solid-allow-automatic-updates" content="false">
```

You might have downloaded a newer version of `index.html`, meaning that the tag is already set but with the default value of `true`. Just change it to `false`, and you're good.

## Upload your front page

Now that you have done the changes you want, you can upload the `index.html` back to your POD:

```
curl --cookie "connect.sid=<your-cookie-value>" --upload-file index.html https://<your-pod>/index.html
```

Visit your front page on your POD to verify that it is uploaded correctly.

If you want to enable automatic updates of your front page, change the value of `solid-allow-automatic-updates` back to true, or remove the meta-tag altogether. It will not be updated until your POD provider runs the `updateindex` script, so you might want to prompt them to do that if it's important for you to get the update as soon as possible.
