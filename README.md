# README

This is a PoC for the EOSC MP Whitelabel solution which allows to define (and later instantiate) a customised MP platform for a community-specific use case. Customisation is scoped to the graphical and content-related elements, the set of functionailites is common and originates from the EOSC Marketplace. Every use case produces a dedicated repo. This customization of the
[EOSC Marketplace](https://github.com/cyfronet-fid/marketplace) is dedicated for the
[EGI](https://www.egi.eu/) use case. 

## How it works - development

The main idea of the customization is to introduce EGI specific colours and
texts. The merketplace logic stays the same. To do the customization you need
to:
  1. clone existing marketplace
     ```
     git clone git@github.com:cyfronet-fid/marketplace.git
     ```
  1. clone this repository
     ```
     git clone git@github.com:cyfronet-fid/egi-marketplace.git
     ```
  1. go to the original marketplace directory and add following ENV variable in
     `.env` directory
     ```
     CUSTOMIZATION_PATH=/path/to/egi-marketplace
     ```

Now you can start original marketplace:
```
# in marketplace directory
./bin/server
```

And start the customization process.

### Customization process

The customization is done by overriding existing marketplace views, locales and
scss files.
```
/egi-marketplace/dir:
  - views          # overrides marketplace/app/views files
  - javascript     # overrides marketplace/app/javascript scss files
  - config/locales # overrides marketplace/config/locales files
```

#### Views
To customize a view find it in the `marketplace/app/views`, copy it into
`egi-marketplace/views` and start the customization. You can use new partials
defined in `egi-marketplace` from overriden view but you cannot create new view.

#### Locales
We are using gettext gem to handle translations. To generate .po files run:
```
rake gettext:add_language[en]
```
...in the original marketplace directory!

If any of the translations changed (in whitelabel or in original marketplace), run:
```
rake gettext:find
```
...which will update the .po files.

To change translations to fit your whitelabel solution, edit .po files:
```
msgid "Original marketplace string"
msgstr "Your string"
```

#### SCSS
**Warning** when new SCSS is added to `egi-marketplace/javascript` directory
rails application needs to be restarted.

**Warning** `marketplace/app/javascript/stylesheets/application.scss` file
cannot be overriden (customization is working only when `@include` scss
directive is used).

To customize a scss file find it in the `marketplace/app/javascript/stylesheets`
directory and copy it into `egi-marketplace/javascript/stylesheets` (the
directory structure need to be the same) and start the customization. Please
rememeber that you need to copy whole file content because original file will
not be loaded if customization file will be found.
