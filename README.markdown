## NinjaScript
NinjaScript is a jQuery library designed to allow unobstrusive scripting simply and easily.  Essentially, we use jQuery selectors to apply behavior the same way we use CSS stylesheets to apply stylings.  Additionally, NinjaScript makes it easy to package up useful behaviors and apply them quickly to disparate elements, or in different projects.

## The Unobtrusive Ideal
Really, unobtrusive scripting is logical extension of the concept of Separation of Concerns.  We haven't put "style" attributes in our HTML since 1998, so why do we still use "onclick"?  Put all your behavior in one place, and you know where to look when you're trying to figure out why it doesn't work.  Plus, it makes it easier to build your site such that it'll work for those benighted souls who don't have Javascript enabled or available.  NinjaScript makes it reasonable to build a site that degrades gracefully.

## Examples

Nothing helps explain this like some examples.  

        <script src="/js/jquery-1.4.js type="text/javascript" />
        <script src="/js/jquery.ninja_script.js" type="text/javascript" />

        <script type="javascript">

        $.behavior({
          "#mail form.new_mail": $.ninja.ajax_submission,
          "#message_list .item": {
            transform: function(elem) {
              $(elem).delay(5000).slideUp(600, function(){$(elem).remove()})
            }
            events: {
              click: function(event, elem) {
                $(elem).remove()
              }
            }
          }
          ".has_tooltip': {
            mouseover: function(event, elem){
              myCreateMouseoverTip(elem)
            }
          }
        })
        </script>

That behavior block sets up three behaviors: 
1. It converts a normal form (could be a POST, GET, whatever) into an AJAX submission.  By default, we'll put a "busy" overlay over the form until we get a response, and add any error messages to a list of error messages.  This behavior is packaged as $.ninja.ajax_submission
1. It adds a decay behavior to messages, using jQuery effects.
1. It applies a tooltip mouseover effect to elements with a "tooltip" class.  We elide the details of what that effect is for the purposes of example.

Notice that behaviors are defined in three different, intermixable styles:
1. Prepackaged, in the form of a method on the Ninja object (available everywhere as $.ninja)
1. With a "transform, events, helpers" syntax, which breaks out everything a behavior can do, completly explicitly.
1. With an abbreviated events form, with the assumption that all we want to do is define a series of event handlers (and possibly a transformer)

## Anatomy of a Behavior

NinjaScript applies "behaviors" to elements selected using jQuery's CSS-like selectors.  A behavior consists of two things: 
0. A transformer: a function called "transform" that take the element as its argument, and changes it in ways that are appropriate to the behavior.  One prepackaged behavior "make_ajax_link" takes a form consisting of a single submit button and converts it into an anchor tag with appropriate attributes.
0. A list of event handlers - functions in two arguments that take action based on the event and thelement.  By default, NinjaScript event handlers swallow the event, preventing the default behavior and preventing the event from bubbling back up the DOM.  You can use an array of [handler_function, *strings] to have NinjaScript allow "default" behavior, allow the event to "propagate", or allow the "immediate" propagation of the event (to other handlers on the same element).

## Mechanics

NinjaScript is designed to be pretty easy to read, but a brief overview of how it works can aid in understanding.  

Going to have to come later though.  I'm going out in about 15 minutes.

