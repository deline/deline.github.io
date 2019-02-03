---
id: 1447
title: Creating an OS X VMware image using Packer
date: 2015-07-22T04:54:44+00:00
author: deline
layout: post
guid: http://delineneo.com/?p=1447
permalink: /2015/07/creating-an-os-x-vmware-image-using-packer/
categories:
  - Technology
---
The time has come to look at OS X VMs. I&#8217;d put this off for a while as the amount of development I&#8217;d have to do on OS X didn&#8217;t warrant the effort. But curiosity, easier management of upgrades and the need to learn new things has spurred me on this path of learning.

So without attempting to chew too much in one go my first attempt is to create a VM image using [Packer](https://www.packer.io/).

Why Packer? From one config you can create images for different platforms &#8211; like VMware, VirtualBox, AWS etc.

For my own learnings I was creating images for VMware.

**Prerequisites**

  1. Have packer installed. If using homebrew simply run <pre class="lang:sh decode:true">brew install packer</pre>

  2. Have [VMware Fusion](https://www.vmware.com/au/products/fusion) or [Fusion Pro](https://www.vmware.com/au/products/fusion-pro/features.html) installed
  3. Clone the [os-x-vm-template](https://github.com/timsutton/osx-vm-templates) project
  4. Have the installation file of OS X available. If you don&#8217;t you can download it as follows:
      * Open App Store
      * Search for the OS &#8211; in my case I looked for &#8216;os x yosemite&#8217;
      * Click download. It&#8217;ll download to /Applications

**Creating the image**

  1. Go to wherever you cloned the os-x-vm-template project.
  2. Run the prepare_iso.sh script <pre class="lang:sh decode:true">sudo prepare_iso/prepare_iso.sh /Applications/Install\ OS\ X\ Yosemite.app output</pre>

    This will finish and chuck out some output similar to:

    <pre class="lang:sh decode:true">-- Fixing permissions..
-- Checksumming output image..
-- MD5: 35a19a9a6462229d203aaa63ef848960
-- Done. Built image is located at output/OSX_InstallESD_10.10.4_14E46.dmg. Add this iso and its checksum to your template.</pre>

  3. Copy the template.json file in the packer directory
    <pre>cp packer/template.json packer/osx-template-vmware-iso.json</pre>

  4. Open the osx-template-vm-ware-iso.json file and:
      * Remove the builder entries for parallels-iso and virtualbox-iso.
      * Modify the iso\_checksum and iso\_url variable values to match the ones spat out in Step 2. E.g.: <pre class="lang:sh decode:true">...
"iso_checksum": "35a19a9a6462229d203aaa63ef848960",
"iso_url": "/Users/deline/Desktop/packer/osx-vm-templates/output/OSX_InstallESD_10.10.4_14E46.dmg",
...</pre>

  5. Validate that your config file looks okay: <pre class="lang:sh decode:true">cd packer
packer validate osx-template-vmware-iso.json</pre>

  6. If your template is all good the next step is to create the image <pre class="lang:sh decode:true">packer build osx-template-vmware-vmx.json</pre>

    This step will take a while as it&#8217;ll create a new VM, install and configure OS X then export it as a new vm. The output will be created in a folder of the same name prefixed with output &#8211; e.g. output-vmware-iso.</li> </ol>

    Next up I&#8217;ll look at using this image as the image as the base source image to create other more specific images. Why do I want to do this? I want the ability to easy trash and recreate OS X environments but I want this to occur fairly quickly. By keeping a base source image I won&#8217;t need to sit through the OS X installation each time I need to start with a &#8216;fresh&#8217; VM.
