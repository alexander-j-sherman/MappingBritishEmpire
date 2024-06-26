This repository contains the files used in the article "Four Theses on the Real and Imaginary British Empire, 1697-1829," along with instructions for how to recreate the maps in Shiny.

The TechnicalAppendix_RealImaginaryEmpire Word document explains how the maps were generated, lists the packages used, shows the sources of the text files, and includes statistics comparing the model's performance to the base Stanford NER and to Matthew Wilkens's 2013 results, repeating some of the explanation from the article.

The MakeMapsInShiny directory includes the scripts to make Shiny maps, the data used to make the maps--mappable versions of the CLIWOC and Slave Voyages data, and a .tsv for each text of all the place names my Stanford NER model identified. The CLIWOC data was restricted to just British voyages; the Slave Voyages data was restricted to British voyages after 1750, and excludes the ports of return.

To view the maps, download the MakeMapsInShiny directory. I suggest installing RStudio, but you can also run R from the command line.

To run the interactive Shiny app and create your own maps, set your working directory to the MakeMapsInShiny directory. Then, run the app:

runApp()
If the command is not recognized, you may need to load the Shiny library:

library(shiny)
There are several packages you may have to download before the app will work.

The Shiny app contains some instructions on making the maps. Note that you may combine multiple texts in one map, but that you may not combine the CLIWOC and Slave Voyages databases nor combine those databases with texts. When combining texts, the raw counts are added together, so long texts (particularly Green's collection) may overwhelm short ones. If you click on a node on the map, the app displays the component place names and their respective counts.

If you would like to examine the data used to make the maps of texts, the script saves it in a global variable, the list SPECIAL; double click on it in the top-right "Global Environment" window of RStudio to see it. Each entry of the list corresponds to a location. The data is still in SPECIAL after you close the Shiny session, so you can manipulate it as well (e.g., sorting by the location with the highest count, seeing how many references to places there are in total in a text).

The script works by calling one of three mapping functions, from the files CLIWOCLeaflet_Final, SVLeaflet_Final, and MakeMapsFromData_Final, since the format of the data for the maps differs across CLIWOC, Slave Voyages, and Stanford NER output. The place names are cross-referenced with NamesAndCoordsRef(NoBlanks).csv to assign coordinates and features (like being a vague place) to them. It is possible to add new mappable texts by adding a .tsv of place names in the same format as the included files (the output from Stanford NER), then by either modifying the app.R script to list their names and files as options, or by directly using the makeMap function from MakeMapsFromData. Given that the reference .csv includes about 3000 places already, it should work well with other eighteenth-century maritime literature, but I would suggest examining the UNMAPPEDPLACES list (currently commented out) in MakeMapsFromData to see how many places you might need to add to NamesAndCoordsRef(NoBlanks).csv to get a useful map. When adding places to NamesAndCoordsREf(NoBlanks), be sure to check whether the location is not already there under a different name (e.g., "China" and "Cathay") or a misspelling, particularly one caused by poor OCR (e.g., "China" and "Chlna").

The SupplementaryFiles directory contains the text files used to make the .tsv files of place names that Stanford NER found in texts, as well as the saved Stanford NER model itself, the training set, and the test set, and a text file of helpful commands in training, testing, and loading a Stanford NER model. I would recommend loading this model if you would like to pull place names from another eighteenth-century maritime text--including text with poor OCR, which the model can handle--but caution that it is wholly untested on other kinds of texts and likely worse than the built-in NER of Stanford CoreNLP or other NER programs. The SupplementaryFiles dirrectory also includes an Excel spreadsheet containing the output of CoreNLP applied to the test set and calculations of its precision, recall, and F-score.
