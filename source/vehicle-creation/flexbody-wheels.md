Flexbody wheels
============

<style type="text/css">
    .smallNumberField {
		background: #D8D8D8;
		color: black;
    }
}
</style>


<script type="text/javascript">

    // version control necessary in case I change the storage format.
    var $version = '0.1';
    // $storage contains all form info in order:
    // version, #wheels, wrays, cnodes, cams
    // in, out, name * max ## wheels used
    var $storage = new Array();
    var $wheelinf = new Array("inside", "outside", "mesh");
    // and $curwheels stores ## of wheels, so updates
    // know how many to attempt to store
    var $curwheels = 0;

    function init() {
        if (localStorage.getItem("storage")) {
            var $local = JSON.parse(localStorage.getItem("storage"));
            if ($local[0] == $version) {
                $storage = $local;
                RetrieveWheels(0);
                BuildFormFields($storage[1]);
                document.getElementById('fillin').innerHTML = "Stored data loaded.";
            }
        }
    }

    function BuildFormFields($amount) {

        var
            $container = document.getElementById('wheelFields'),
            $item, $field, $i;
        WriteWheels($curwheels);
        // do this after saving whatever exists.
        $curwheels = $amount;

        $container.innerHTML = '';
        for ($i = 0; $i < $amount; $i++) {
            $item = document.createElement('div');
            $item.style.margin = '3px';

            $field = document.createElement('span');
            $field.innerHTML = 'Wheel ' + ($i + 1) + ':<br \> inside axle node';
            $field.style.marginRight = '10px';
            $item.appendChild($field);

            $field = document.createElement('input');
            $field.id = 'inside[' + $i + ']';
            $field.type = 'text';
            $field.style.background = '#D8D8D8';
            $field.style.color = 'black';
            $field.size = 3;
            $item.appendChild($field);

            $field = document.createElement('span');
            $field.innerHTML = 'outside axle node';
            $field.style.margin = '0px 10px';
            $item.appendChild($field);

            $field = document.createElement('input');
            $field.id = 'outside[' + $i + ']';
            $field.type = 'text';
            $field.style.background = '#D8D8D8';
            $field.style.color = 'black';
            $field.size = 3;
            $item.appendChild($field);

            $field = document.createElement('span');
            $field.innerHTML = 'mesh name';
            $field.style.margin = '0px 10px';
            $item.appendChild($field);

            $field = document.createElement('input');
            $field.id = 'mesh[' + $i + ']';
            $field.type = 'text';
            $field.style.background = '#D8D8D8';
            $field.style.color = 'black';
            $field.size = 15;
            $item.appendChild($field);
            $container.appendChild($item);
        }
        RetrieveWheels($curwheels);

    }

    function GenerateCode($form) {

        var $output = document.getElementById('fillin');
        var $wrays = parseInt(document.getElementById('wrays').value, 10);
        var $wheels = parseInt(document.getElementById('wheels').value, 10);
        var $cnodes = parseInt(document.getElementById('cnodes').value, 10);
        var $cams = parseInt(document.getElementById('cams').value, 10);
        var $field, $item;
        $field = document.createElement('span');
        $field.innerHTML = 'flexbodies <br \>';
        $field.type = 'text';
        $output.innerHTML = '';
        $output.appendChild($field);
        var $in, $out, $name, $node, $i;

        $node = $cnodes + $cams;
        for ($i = 0; $i < $wheels; $i++) {
            $text = '; wheel ' + ($i + 1) + '\n';
            $in = parseInt(document.getElementById('inside[' + $i + ']').value, 10);
            $out = parseInt(document.getElementById('outside[' + $i + ']').value, 10);
            $name = document.getElementById('mesh[' + $i + ']').value;
            $text = $text + $in + ', ' + $out + ', ' + ($node + 1) + ', 0, 0, 0, 0, 0, 0, ' + $name + '\n';
            $text = $text + 'forset ' + $out + ', ' + $in + ', ' + ($node + 1) + '-' + ($node + 2 * $wrays) + '\n\n';
            $node = $node + 2 * $wrays;
            $field = document.createTextNode($text, false);
            $output.appendChild($field);
        }
        WriteWheels($wheels);
        localStorage.setItem("storage", JSON.stringify($storage));

    }

    function WriteWheels($nwhl) {
        // WriteWheels moves current form info into the array

        // $storage contains all form info in order:
        // #wheels, wrays, cnodes, cams
        // in, out, name * max ## wheels used
        $storage[0] = $version;
        $storage[1] = document.getElementById('wheels').value;
        $storage[2] = document.getElementById('wrays').value;
        $storage[3] = document.getElementById('cnodes').value;
        $storage[4] = document.getElementById('cams').value;
        var $i, $j;
        for ($i = 0; $i < $nwhl; $i++) {
            for ($j = 0; $j < $wheelinf.length; $j++) {
                $storage[$wheelinf.length * $i + 5 + $j] = document.getElementById($wheelinf[$j] + '[' + $i + ']').value;
            }
        }
    }

    function RetrieveWheels($nwhl) {

        // RetrieveWheels moves array into current form info.
        // first the static ones
        document.getElementById('wheels').value = $storage[1];
        document.getElementById('wrays').value = $storage[2];
        document.getElementById('cnodes').value = $storage[3];
        document.getElementById('cams').value = $storage[4];
        var $i, $j;
        var $len = ($storage.length - 5) / $wheelinf.length;
        for ($i = 0; $i < Math.min($nwhl, $len); $i++) {
            for ($j = 0; $j < $wheelinf.length; $j++) {
                document.getElementById($wheelinf[$j] + '[' + $i + ']').value = $storage[$wheelinf.length * $i + 5 + $j];
            }
        }

    }

</script>

<form method="post">
    Number of wheels <input type="text" id="wheels" class="smallNumberField" onkeyup="BuildFormFields(parseInt(this.value, 10)); ">
    <br>Wheel rays <input type="text" class="smallNumberField" id="wrays">
    <br>Chassis nodes <input type="text" class="smallNumberField" id="cnodes">
    <br>Cameras before wheel section <input type="text" class="smallNumberField" id="cams">
    <div id="wheelFields" style="margin:20px 0px; "></div>
    <input type="button" value="Generate code" class="smallNumberField" onclick="GenerateCode(this.form)">
</form>
<div id="fillin" style="white-space: pre; font-family: monospace; ">
</div>

<script type="text/javascript" src="/scripts/json2.js"></script>
<script type="text/javascript">
    var readyStateCheckInterval = setInterval(function () {
        if (document.readyState === "complete") {
            init();
            clearInterval(readyStateCheckInterval);
        }

    }, 10);
</script>

## What is this?

By default, Rigs of Rods's [meshwheels](/vehicle-creation/fileformat-truck/#meshwheels) sections generate a tire using a texture. In order to use a 3D tire mesh, you have to place the tire meshes using [flexbodies](/vehicle-creation/fileformat-truck/#flexbodies) or [props](/vehicle-creation/fileformat-truck/#props). This tool simplifies that process by generating the flexbody code for you.

Some addon parts require you to generate flexbody wheels as the tire mesh is separate.

Not to be confused with [flexbodywheels](/vehicle-creation/fileformat-truck/#flexbodywheels), which provides this feature.

## Instructions

First, make sure the tire material in the meshwheels section is set to `tracks/trans` , for example:

```
meshwheels
;tire_radius, rim_radius, width, numrays, node1, node2, snode, braked, propulsed, arm,  mass,   spring, damping, side,               meshname         material
0.35,       0.21,   0.5,      14,    32,    33,    34,      1,         1,  18, 200.0, 300000.0,  2000.0,    l, dodgechargerwheel.mesh tracks/trans
0.35,       0.21,   0.5,      14,    34,    35,    33,      1,         1,  26, 200.0, 300000.0,  2000.0,    r, dodgechargerwheel.mesh tracks/trans
0.35,       0.21,   0.5,      14,    44,    45,  9999,      1,         0,  53, 200.0, 350000.0,  2000.0,    l, dodgechargerwheel.mesh tracks/trans
0.35,       0.21,   0.5,      14,    46,    47,  9999,      1,         0,  50, 200.0, 350000.0,  2000.0,    r, dodgechargerwheel.mesh tracks/trans
```

Notice the `tracks/trans` at the end of the line. This makes the default tire invisible.

Explanation of each option:

`Number of wheels` - Amount of wheels the vehicle has.

`Wheel rays` - The number of ‘pie pieces’, or corners, that make up the wheel. In the above example, `numrays` is set to `14` .

`Chassis nodes` - Amount of nodes the vehicle has. Just set the last node ID at the bottom of the [nodes](/vehicle-creation/fileformat-truck/#nodes) section.

`Cameras before wheel section` - Amount of [cameras](/vehicle-creation/fileformat-truck/#cameras) the vehicle has. Most only have 1, while others (such as the Gavrils) have 3.

`Inside axle node` -  The inner axle node. In the above example, the first wheel's `node1` is `32` .

`Outside axle node` - The outer axle node. In the above example, the first wheel's `node2` is `33` .

`Mesh name` - The mesh name of the tire, with `.mesh` file extension.

Once you fill in all options, click `Generate code` to generate the flexbodies.

All that's left to do is just paste the generated flexbody lines below the `meshwheels` section.

Complete example for the Burnside Race:

```
meshwheels2
;tire_radius, rim_radius,width,numrays,node1,node2,snode,braked,propulsed, arm, mass, spring, damping, side, meshname material
0.35, 0.233, 0.265, 14, 44, 46, 9999, 4, 1, 131, 46.0, 100000.0, 900.0, r, ICD_AEZ_Forged_16.mesh tracks/trans
0.35, 0.233, 0.265, 14, 45, 47, 9999, 4, 1, 134, 46.0, 100000.0, 900.0, l, ICD_AEZ_Forged_16.mesh tracks/trans
set_beam_defaults 3300000, 90, 2000000, 2500000
set_node_defaults -1, 1.14, -1, -1
0.35, 0.233, 0.265, 14, 66, 67, 69, 1, 1, 62, 46.0, 125000.0, 900.0, r, ICD_AEZ_Forged_16.mesh tracks/trans
0.35, 0.233, 0.265, 14, 69, 70, 67, 1, 1, 63, 46.0, 125000.0, 900.0, l, ICD_AEZ_Forged_16.mesh tracks/trans

flexbodies
; wheel 1
44, 46, 249, 0.5, 0, 0, 0, 0, 0, ICD_Kumho_ECSTA_SPT_16.mesh
forset 46, 44, 249-276

; wheel 2
45, 47, 277, 0.5, 0, 0, 0, 0, 0, ICD_Kumho_ECSTA_SPT_16.mesh
forset 47, 45, 277-304

; wheel 3
66, 67, 305, 0.5, 0, 0, 0, 0, 0, ICD_Kumho_ECSTA_SPT_16.mesh
forset 67, 66, 305-332

; wheel 4
69, 70, 333, 0.5, 0, 0, 0, 0, 0, ICD_Kumho_ECSTA_SPT_16.mesh
forset 70, 69, 333-360
```

When you click `Generate code` , the current settings attempt to be
stored in the browser, so that when revisiting the page, they are retrieved.

This only allows storage of one truck's settings at a time - hopefully that's
enough for development purposes.

## Troubleshooting

* If the tire sticks too far out/in, adjust the [X offset](/vehicle-creation/fileformat-truck/#flexbodies). In the above Burnside Race example, the offset is set to `0.5` .

* If the tire glitches/isn't attached to the wheel, you have set the wrong node/camera count and/or wheel nodes.

## Credits

This was originally a spreadsheet by Fat-Alfie on the
 [Rigs of Rods](https://forum.rigsofrods.org/) forum.  Translated  into html/javascript form by nmurdoch.ca to make it more convenient.
