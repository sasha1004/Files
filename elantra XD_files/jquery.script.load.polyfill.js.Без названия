/**
 * Отлавливаем ошибки на этапе загрузки jsonp через jquery
 */
jQuery.ajaxTransport('+script', function(s) {
  // This transport only deals with cross domain requests
  if (s.crossDomain) {
    var script,
      head = document.head || document.getElementsByTagName('head')[0] || document.documentElement;
    return {
      send: function( _, callback ) {
        script = document.createElement('script');
        script.async = 'async';
        if (s.scriptCharset) {
          script.charset = s.scriptCharset;
        }
        script.src = s.url;
        // Attach handlers for all browsers
        script.onload = script.onreadystatechange = function(_, isAbort) {
          if (isAbort || !script.readyState || /loaded|complete/.test(script.readyState)) {
            // Handle memory leak in IE
            script.onload = script.onreadystatechange = null;
            // Remove the script
            if (head && script.parentNode) {
              head.removeChild(script);
            }
            // Dereference the script
            script = undefined;
            // Callback if not abort
            if (!isAbort) {
              callback(200, 'success');
            }
          }
        };
        script.onerror = function(err) {
          callback(err.type, err.type, err);
        };
        head.insertBefore(script, head.firstChild);
      },
      abort: function() {
        if (script) {
          script.onload(0, 1);
        }
      }
    };
  }
});