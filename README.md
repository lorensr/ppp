Background: [Purchasing power parity](https://en.wikipedia.org/wiki/Purchasing_power_parity)

`npm install @lorensr/ppp`

If we had a product that cost $50 USD in the United States, and we had a customer in India, then we would charge them 26.5% of the full cost—$13.27 USD:

```js
import getPpp from '@lorensr/ppp'

const originalPrice = 50;
const countryCode = 'IN'

getPpp(countryCode).then(ppp => {
  const discountPrice = ppp.pppConversionFactor * originalPrice
  console.log(discountPrice)
  console.log(ppp)
});
```

```js
13.2690310135
{ currenciesCountry: [ { code: 'INR', name: 'Indian rupee', symbol: '₹' } ],
  countryCodeIsoAlpha3: 'IND',
  currencyMain:
   { exchangeRate: 67.39,
     code: 'INR',
     name: 'Indian rupee',
     symbol: '₹' },
  ppp: 17.884,
  pppConversionFactor: 0.26538062027006976 }
```

We recommend running this code on the server, as deciding pricing on the client is insecure. To determine the client's location, you can use their IP address and a geolocation API like [ipstack](https://ipstack.com/), or if you use Cloudflare, you use their [`CF_IPCOUNTRY` HTTP header](https://support.cloudflare.com/hc/en-us/articles/200168236-What-does-Cloudflare-IP-Geolocation-do-), which contains the client's country code. The latter method is less able to be tricked by proxies and VPNs.