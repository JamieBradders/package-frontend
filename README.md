# Package Frontend

Serves as a visual Web Browser for the [`package-backend`](https://github.com/pulsar-edit/package-backend).

Currently this matches very closely with the design of the original package viewer from upstream Atom.

Although does fully support multiple themes being added on later with a theme switcher.

The Web Browser for Packages is available on [`pulsar-edit.dev`](https://web.pulsar-edit.dev/).

If you'd like to read about some of the challenges of normalizing the data across so many different Packages:

  * [Repository URLs](/docs/repository-urls.md)
  * [Authors](/docs/authors.md)
  * [Links](/docs/links.md)

---

When browsing the website, if you'd like to investigate what's caused the page load to take a long time there's now a built in utility to help determine that. While it can't show every aspect of the page load it could at least help to rule out some aspects.

When on the website, open the DevTools for your respective browser and in the provided console type:

```javascript
loadStats();
```

This will output similar to the following:

```json
{
  "api-request": {
    "duration": 922.325,
    "end": 2699.609,
    "start": 1777.28
  },
  "transcribe-json": {
    "duration": 14.55,
    "end": 2714.175,
    "start": 2699.617
  }
}
```

Of the above output, the only field that you should worry about is `duration`, as this tells you in milliseconds how long whatever action is related took. Of the actions that might be shown below is an explaination of what they mean.

* `api-request`: An API Request was needed to be made to the backend server, and this shows the duration that request took.
* `transcribe-json`: JSON Data received from an API request needs to be modified to be displayed to the end user, and some of these actions are intensive. This shows the duration it took to completly modify and return the JSON data.
* `cache-check`: Local or Remote or Both types of caching are implemented on this endpoint. This shows the duration it took to check with said caches for the relevant data.

Currently `loadStats()` is unable to display how long certain actions took, which are listed below:

* The time `ExpressJS` took to handle the request itself.
* The time `PugJS`/`Jade` templates took to handle creating and displaying the page.
