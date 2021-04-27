# timer-app

## Description
A simple vuejs application that allows you to run multiple timers at the same time. The application solves the problem of calculating the time when the current tab is not active. Because setInterval and setTimeout methods suspened when tab not active, also Chrome have limitation 1000ms for background threads. It uses RXJS and timestamp for resolve this issue.
##

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
