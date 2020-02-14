# README

This is an customization of the
[Marketplace](https://github.com/cyfronet-fid/marketplace) for the
[EGI](https://www.egi.eu/).

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
Find a key in original marketplace you wan to override and create yaml file in
`egi-marketplace/config/locales` directory. The name of the file doesn't have to
match original yaml file name but it is a good practice to keep naming
convention used in the `marketplace`.

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
