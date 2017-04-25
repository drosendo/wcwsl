# wcwsl
WooCommerce Software License - Helper

This is for anyone using WooCommerce Software License that wants to integrate the autoupdate and license register/validation to their plugin.

Any help on improving this is welcomed.

# Install

Just put the wcwsl.php into your plugin folder and include it so that is runs.

## Get license
```
get_option('wcwsl_softlicense_key');
```

## Ajax register license Example

```
jQuery.ajax({
    url: ajaxurl,
    type: 'post',
    dataType: 'json',
    data: {
        action: 'wcwsl_licenseverify',
        data: $('input#wcwsl_license').val()
    },
    success: function (response) {

        if (response.status && response.status != 'warning') {

            $('form#wcwsl_license').append('<div class="notice notice-success is-dismissible">' + response.message + '. Page wil reload shorthly.</div>');
            setTimeout(function () {
                $('.notice.notice-success').slideUp('fast').fadeOut(function () {
                    window.location.reload();
                });
            }, 2500);
        } else if (response.status == 'warning') {
            $('form#wcwsl_license').append('<div class="notice notice-warning is-dismissible">' + response.message + '</div>');
        } else {
            $('form#wcwsl_icense').append('<div class="notice notice-error is-dismissible">' + response.message + '</div>');
        }

    }
});
```

### Other actions in wcwsl.php

Thanks,
David
