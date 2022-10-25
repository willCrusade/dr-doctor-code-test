#Please copy .env.example to .env to use the endpoint

###run yarn

you know the drill

Notes:

No time to finish off UI or validation,

This is what I would have done for validation:

- Max length is set to 50 for the last name already
- For the postcode i'd have set a maxlength and used `/^[a-z0-9]+$/i` regex to check if it was alphanumeric
- For the date I'd have used `Date.parse()` to confirm it was indeed a date