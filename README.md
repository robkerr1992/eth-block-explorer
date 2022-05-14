# eth-block-explorer
A really basic implementation of and Ethereum block explorer using Nuxt.

To get this running locally you'll first need to create a env file.
```bash
echo "PROVIDER_URL=" > .env
```

Now you need a provider url, I used [Alchemy](https://www.alchemy.com). Create an account and grab an http key from a created app consuming your desired network (If you're not sure which try the Main Chain). Copy the url and fill in your .env file like this:
```
PROVIDER_URL=your.url
```

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev
```

Navigate the `localhost:3000` in your favorite browser and it should be working!

This was my first time using Nuxt. There was a bit of a learning curve but overrall it was a good experience!

Tech used in this project:
- [Vue](https://vuejs.org/)
- [Nuxt](https://nuxtjs.org/)
- [Tailwind](https://tailwindcss.com/)
- [Ethers](https://docs.ethers.io/v5/)

## Features

- View block data and the first 10 transactions from the most recently mined Ethereum block
- Click a transaction hash to view some more details about the transaction
- Click the `Refresh` button to view the most up to date information on the latest block