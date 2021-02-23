## Data Requests with `wget`

All zips: `wget "https://data.cityofchicago.org/resource/553k-3xzc.json?\$select=:*,%20*&\$order=date%20DESC&\$limit=10000"`

That includes system values (`:*`), including when the records were last updated (`:updated_at`),
and orders all records descending by date (i.e., most recent first). As of February 23, 2021, there
are 4000+ records in the set, so the limit of 10000 is a placeholder. Unclear how to set limit to
always grab all records; without the `limit` parameter, 1000 records are returned.

## Snooping for Cross-Referenced Data Sets

Some APIs return references to other data sets, e.g.,

```json
":@computed_region_vrxf_vc4k":"38",
":@computed_region_6mkv_f3dw":"14309",
":@computed_region_bdys_3d7i":"580",
":@computed_region_43wa_7qmu":"36",
":@computed_region_rpca_8um6":"42"
```

An easy way to figure out what the 8-digit code at the end refers to, like `vrxf_vc4k` is to stick
them onto the end of this URL: `https://data.cityofchicago.org/d/`. So to look up `vrxf_vc4k`,
change the underscore, `_`, to a hyphen and go to https://data.cityofchicago.org/d/vrxf-vc4k.

Another note is that the values on the `:@computed_region` values point to **records** in the
corresponding set, and not to a useful human value. For example, the Wards set at
https://data.cityofchicago.org/dataset/Wards/43wa-7qmu has a value of `36` above, but does **not**
refer to to 36th Ward, but the ward at ID `36` (which just happens to be Ward 42; see https://data.cityofchicago.org/resource/43wa-7qmu.json?_feature_id=36).
