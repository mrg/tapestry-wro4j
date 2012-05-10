# Tapestry WRO4J

[![Build Status](http://travis-ci.org/lltyk/tapestry-wro4j.png)](http://travis-ci.org/lltyk/tapestry-wro4j)

Adds support for various
[Web Resource Optimizer](http://code.google.com/p/wro4j/) components to
Tapestry 5.3.

Included are various choices of JavaScript and CSS minifiers, and
Less/Sass/Coffeescript transformers.

## Usage

The transformers automatically associate with their file extensions, simply
create one (a .coffee file for example), and include it on a page just as you
would a js file:

    @Import(library="somefile.coffee",stylesheet="someotherfile.less")

By default, Google Closure Compiler is used for JS minimization, and YUI is
used for CSS. Other choices for JS include UglifyJSMinimizer and
YuiJSMinimizer. You can use one instead with this in your AppModule:

    @Contribute(ResourceMinimizer.class)
    @Primary
    public static void contributeMinimizers(MappedConfiguration<String, ResourceMinimizer> configuration)
    {
      configuration.overrideInstance("text/javascript", UglifyJSMinimizer.class);
    }

By default Tapestry only enables minification when the tapestry.production-mode
flag is set. You can enable it manually in your AppModule like so:

    public static void contributeApplicationDefaults(MappedConfiguration<String, String> configuration)
    {
      configuration.add(SymbolConstants.MINIFICATION_ENABLED, "true");
    }

WRO4J's WroFilter will be automatically enabled (without having to add it in
web.xml) if a wro configuration file is found. Other WRO4J features that are
not automatically enabled can be added manually this way. For example, if the
following wro.groovy file is present in WEB-INF, assets at
/contextpath/wro/all.js and /contextpath/wro/all.css become available:

    groups {
      all {
        js "/js/**.js"
        css "/css/**.css"
      }
    }
This can be turned off with the WRO4JSymbolConstants.AUTO_ENABLE_WRO_FILTER
symbol.

## 0.9.5
Tapestry 5.3.3  
Added symbols for disabling automatic adding of transformers in WRO4JSymbolConstants  
Added automatic registration of WroFilter without having to modify web.xml  
Tweaked RequireJS support  

## 0.9.4
WRO4J 1.4.5  
Experimental RequireJS support  

## 0.9.3
WRO4J 1.4.4  

## 0.9.2
Tapestry 5.3.2  

## 0.9.1
Automatically included WRO4JModule in jar manifest.  
Added Google Closure for JS and YUI for CSS as default minimizers.  
Fixed UglifyJS/Prototype interoperability.  
Fixed Less import support (issue #2)  
WRO4J 1.4.3  

## 0.9
Initial Release  
WRO4JModule needs to be included manually with @SubModule.  
Minifiers need to be added manually using contributeMinimizers.  
WRO4J 1.4.2  
