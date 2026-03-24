# AIESEC Embeddable Auth
Demo: https://embeddable-auth.netlify.com/ (Running staging environment)

**Importing**: If you are using it with any app having npm, run
```shell
$ npm install @commutatus/aiesec-embeddable-auth --save
```

In your app:
```js
import '@commutatus/aiesec-embeddable-auth'
```

Use css from

`node_modules/@commutatus/aiesec-embeddable-auth/bundle.css`

For all other use cases:

Load the script from

`https://unpkg.com/@commutatus/aiesec-embeddable-auth@latest/bundle.js`

and the CSS from

`https://unpkg.com/@commutatus/aiesec-embeddable-auth@latest/bundle.css`

## Usage

HTML:
```html
<div id="embeddable-auth-container"></div>
```


Javascript:
```js
const embeddableAuth = new EmbeddableAuth({
	target: document.getElementById('embeddable-auth-container'),
	props: {
		options: {
			registerButtonText: 'Get Started',
			loginButtonText: 'Login',
			defaultReferral: 'Other',
			afterLoginRedirectTo: '',
			title: 'Login/Register with AIESEC',
			showLogin: true,
			utm: {
				utm_source: 'your-utm-source-value',
				utm_medium: 'your-utm-medium-value',
				utm_campaign: 'your-utm-utm_campaign-value',
				utm_term: 'your-utm-utm_term-value',
				utm_content: 'your-utm-utm_content-value',
			},
			customMeta: {
				yourCustomField1: yourCustomValue1,
				yourCustomField2: yourCustomValue2
			},
			profileAttributes: {
				// See the next section for more info
			},

		},
		token: 'YOUR_TOKEN', // custom token for future features.
		api: 'production' // or 'staging'  MANDATORY
	}
});
```

| Option | Default Value | Description | Type |
|---|---|---|---|
| registerButtonText | Get Started | Text of the register button | string |
| loginButtonText | Login | Text of the login CTA button | string |
| defaultReferral |  | Default value for referral (If used, the referral selection won't be shown to the user) | string |
| afterLoginRedirectTo |  | Url to redirect to after login or signup succeeded (without root domain) Example: 'opportunity/5999' | string |
| title | Login/Register with AIESEC | Heading of the container. This appears above the register/login title. Disabled if `false` | string or `false` |
| showLogin | `true` | Whether it should default to login screen. Signup screen will be shown by default if `false` | boolean |
| allowPhoneCommunication | `false` | Whether phone number can be used for communication. Phone number will not be shown on admin dashboard if `false` | boolean |
| loginFormTitle | Login | Title for the login form. Disabled if `false` | string or `false` |
| registerFormTitle | Register | Title for the signup form. Disabled if `false` | string or `false` |
| disableFormToggle | `false` | Do not allow user to switch between the register and the login form. Enabling this hides the button to switch between forms | boolean |
| useModalLayout | `true` | Controls whether the auth should be shown inside a modal or inside the target element itself | boolean


If you are using `defaultReferral`, please use one of these values given below:

```
Friend, Colleague, Information booth on campus, Classroom presentation, AIESEC Alumni, Facebook, WeChat, Twitter, Instagram, LinkedIn, , Other social media channel, Search Engine, Event, Telegram, Media (magazine, TV, newspaper or radio), Other
```

For **profileAttributes**, the data structure should be as follows. Note that this will not support any other field not mentioned in the structure given below.

```
{
	person_profile_attributes: {
		earliest_start_date: "dd-mm-yyyy",
		latest_end_date: "dd-mm-yyyy",
		duration_min: 6, // Number of weeks
		duration_max: 78, // Number of weeks
		languages: [
			10005,
			10006
		],
		nationalities: [1034],
		selected_programmes: [1],
		skills: [
			{
				id: 10147
			},
			{
				id: 10146
			}
		]
	}
}
```

The ID's which are passed in languages, nationalities and skills can be get from constants endpoints hyperlinked here [Languages Nationalities Skills](https://gis-api.aiesec.org/v2/lists/nationalities.json?access_token=e316ebe109dd84ed16734e5161a2d236d0a7e6daf499941f7c110078e3c75493)

For selected_programmes, the values are

|Name | Value |
|--|--|
|GV|7|
|GT|8|
|GE|9|