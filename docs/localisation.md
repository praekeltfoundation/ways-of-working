# Localisation

Localisation is important at Praekelt - all our projects need to be accessible
by as many people as possible.

Every project will need to support a different set of languages depending on
its users.

## ISO 639-3

We prefer ISO 639-3 codes for languages. Wikipedia has a
[list of ISO 639-3 codes][iso-639-3-codes].

In HelloMama, we join the ISO 639-3 three character language code with the
[ISO 3166-1 alpha-2][iso-3166-1-alpha-2] two character country code. For example:

- `eng_NG`: English - Nigeria
- `eng_ZA`: English - South Africa
- `pcm_NG`: Pidgin - Nigeria

## ISO 639-2

Wikipedia has a [list of ISO 639-2 codes][iso-639-2-codes].

### RapidPro

As of January 2017, [RapidPro uses ISO 639-2 but has plans to move to 639-3][rapidpro-lang].

They acknowledge that 639-2 is incomplete for African dialects. If there isn't a specific
language code available, we choose one from 639-2 that starts with the same letter and is
"close" to the name of the language we want to use. At the moment we use:

```
| Code   | Actual meaning     | Praekelt meaning |
| ------ | ------------------ | ---------------- |
| ach    | Acholi or Acoli    | same             |
| lin    | Lingala            | same             |
| lus    | Lushai             | ?                |
| nau    | Nauru              | ?                |
| rar    | Cook Islands Maori | ?                |
| rom    | Romany             | ?                |
| run    | Rundi              | same             |
| wel    | Welsh              | ?                |
```

[rapidpro-lang]: https://groups.google.com/d/topic/rapidpro-dev/v6eASOWCMPA/discussion
[iso-639-2-codes]: https://en.wikipedia.org/wiki/List_of_ISO_639-2_codes
[iso-639-3-codes]: https://en.wikipedia.org/wiki/List_of_ISO_639-3_codes
[iso-3166-1-alpha-2]: https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
