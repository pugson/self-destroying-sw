# Self-destroying ServiceWorker

Code-snippets and guides on removing ServiceWorker from a websiste.

## Motivation

ServiceWorker is more and more often used in websites development. It’s being added to popular tools and libraries. Sometimes, it might be used unintentionally (generated by a pre-configured tool automatically) or for experimental purposes. This leads to a situation where ServiceWorker needs to be removed.

[Read more on Medium](https://medium.com/@nekrtemplar/self-destroying-serviceworker-73d62921d717)


## How to use

1. Remove everything about your previous ServiceWorker (registration/uninstallation code, ServiceWorker file)
2. Create a file with the same name as your previous ServiceWorker and put it in the same place where your previous ServiceWorker was
3. Put following code into the file:


```js
self.addEventListener('install', function(e) {
  self.skipWaiting();
});

self.addEventListener('activate', function(e) {
  self.registration.unregister()
    .then(function() {
      return self.clients.matchAll();
    })
    .then(function(clients) {
      clients.forEach(client => client.navigate(client.url))
    });
});
```

4. Deploy your project! 🎉

[With webpack](packages/webpack-remove-serviceworker-plugin) | [With Gatsby](packages/gatsby-plugin-remove-serviceworker)


## License

MIT