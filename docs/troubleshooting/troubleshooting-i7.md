# Troubleshooting in Islandora 7

Troubleshooting documentation is currently scattered around https://arca.bcelnapps.ca.

This document will be an attempt to consolidate that information. It will be obsolete after the migration.

## Display
<details>
<summary>How can I change the repository name in my breadcrumbs?</summary>
<br>

>To batch export datastreams for newspaper issues, use the Islandora Datastreams I/O (information in [this Arca Minute](https://youtu.be/hjBRml74_eY)). Select the Solr Query option and enter the following text: `RELS_EXT_isMemberOf_uri_mt:"PID"` (replacing `"PID"` with the PID for the newspaper collection). This will export all of the child objects for that newspaper. For example, to make batch metadata edits, select the MODS datastream.
  
</details>
<details>
<summary>How do I control how my collections are sorted?</summary>
<br>

>You can use Solr fields to determine how your collections' objects are sorted.
>1. Make sure that your Collection Solution Pack is configured to use Solr for display generation (admin/islandora/solution_pack_config/basic_collection)
>2. Under “Sort field for collection query”, enter your chosen field followed by `asc` or `desc`. For dates, use the `_dt` version of the field. For other field types, use `_ss`.
>    - Use `mods_titleInfo_title_ss asc` to sort by title A-Z.
>    - Use `mods_originInfo_dateIssued_dt desc` to sort by date, newest to oldest.
>3. If you want to be able to configure different sort strings for individual collections, check “Allow individual sort strings per collection”
>    1. Manage the collection that you want to sort differently
>    2. On the Collection tab, choose Set Solr Sort String
>    3. Enter a sortable string (ends with `_ss`) followed by `asc` or `desc` to use for sorting this collection.
>4. If you want to use the Islandora Sort block to allow multiple sort fields, enable it at Structure -> Blocks. Choose the sort fields under "Sort Settings" in the Solr configuration screen (admin/islandora/search/islandora_solr/settings).
</details>
<details>
<summary>Metadata display changes for Citation/Thesis objects don't take effect</summary>
<br>

>If you're making changes to you Citation or Thesis objects' metadata display profiles (at Islandora -> Solr Index -> Metadata display), check our Scholar configuration.
>  
>Go to Islandora -> Solution Pack Configuration -> Scholar. Scroll down to find the option "Use Standard Metadata Display". Make sure it is checked.
>  
>Scholar defaults to its own metadata display, [COinS](https://en.wikipedia.org/wiki/COinS). This display is not configurable, and so is probably not the best choice for objects in Arca.
</details>
<details>
<summary>One of my display fields shows multiple values instead of just one. How do I fix it?</summary>
<br>

>When viewing an object, one or more of the metadata display fields shows several values in it, from several different elements that were added separately to the ingest form. How can I display one specific value?
>  
>Your metadata display profile (or Solr search result field, or wherever you're using a Solr field) is probalby using the Dublin Core Solr field (`dc.description`, `dc.identifier`, etc.) rather than the more granular MODS Solr field. Dublin Core is not as precise as MODS, and many DC elements combine different MODS elements into one.
>  
>For example, dc.description will combine MODS abstract, and all MODS note elements. If you want to display just one of these, choose the MODS field that contains the specific piece of metadata you require.
</details>
<details>
<summary>My object doesn't display the fields I want. Do I need to change the ingest form?</summary>
<br>

>No!
>  
>Your ingest form is probably fine. Solr generates many fields based on the metadata you ingest via the form, and your object's content model metadata display profile is only configured to display a certain selection of those. You can configure the fields used in your Solr Metadata Display in admin/islandora/search/islandora_solr/metadata.
>  
>For detailed assistance with this, including ways to find out which fields you should be using, review the [Metadata Display Arca Hour](http://ac-connect.bccampus.ca/p34d7sm0zb7/).
</details>
