Welkom bij de Android APS documentatie
==================================================

AndroidAPS is een open source app voor mensen met insuline-afhankelijke diabetes. De app fungeert als een kunstmatig alvleesklier systeem (APS, Artificial Pancreas System) op Android smartphones. Belangrijkste componenten zijn verschillende OpenAPS software algoritmen die doen wat een levende alvleesklier doet: de bloedsuiker binnen gezonde grenzen houden. Het algoritme doet dit door het gebruik van geautomatiseerde insulinedosering (AID, Automated Insulin Dosing). Daarnaast is een door de app ondersteunde en FDA/CE goedgekeurde insulinepomp en een continue glucosesensor nodig. 

De app gebruikt GEEN zelflerende kunstmatige intelligentie. In plaats daarvan zijn de berekeningen van AndroidAPS gebaseerd op de individuele insulinebehoefte en de inname van koolhydraten die de gebruiker handmatig invoert, maar ze worden om veiligheidsredenen door het systeem gecontroleerd. 

De app is niet verkrijgbaar in de Google Play store - om juridische redenen moet iedere gebruiker de app zelf vanuit de broncode bouwen.

De belangrijkste onderdelen zijn:

.. image:: images/modules-female.png
  :alt: Onderdelen

Hieronder volgt de inhoudsopgave.

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Taal wijzigen

   Taal wijzigen <./changelanguage.rst>

.. _Aan de slag:

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Aan de slag

   Allereerst de veiligheid <./Getting-Started/Safety-first.rst>
   Wat is een closed loop systeem <./Getting-Started/ClosedLoop.rst>
   Wat is een closed loop systeem met AndroidAPS <./Getting-Started/WhatisAndroidAPS.rst>  
   Insulinepompen <./Getting-Started/Pump-Choices.md>
   Documentatie wijzigingen <./Getting-Started/WikiUpdate.rst>

.. _wat-heb-ik-nodig:

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Wat heb ik nodig? 

   Onderdelen <./Module/module.rst>

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: AndroidAPS installeren

   Bouwen van de app <./Installing-AndroidAPS/Building-APK.md>
   Bijwerken naar een nieuwe versie <./Installing-AndroidAPS/Update-to-new-version.md>
   Hints and Checks after update to AAPS 3.0<./Installing-AndroidAPS/update3_0.md>
   Controles na bijwerken naar AAPS 2.7 <./Installing-AndroidAPS/update2_7.rst>
   Git installeren <./Installing-AndroidAPS/git-install.rst>
   Problemen in Android Studio oplossen <./Installing-AndroidAPS/troubleshooting_androidstudio.rst>
   Release notes <./Installing-AndroidAPS/Releasenotes.rst>
   Dev branch (voor ontwikkelaars) <./Installing-AndroidAPS/Dev-branch.md>

.. _onderdelen-instellen:

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Onderdelen instellen

   BG bron <./Configuration/BG-Source.rst>
   xDrip+ instellingen <./Configuration/xdrip.md>
   Pompen <./Hardware/pumps.rst>
   Telefoons <./Hardware/Phoneconfig.rst>
   Nightscout instellen <./Installing-AndroidAPS/Nightscout.md>
   Smartwatch <./Hardware/Smartwatch.rst>

.. _configuratie:

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Configuratie

   Configurator <./Configuration/Config-Builder.md>
   Instellingen <./Configuration/Preferences.rst>

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: AndroidAPS gebruiken

   AndroidAPS Screenshots <./Getting-Started/Screenshots.md>
   Doelen <./Usage/Objectives.rst>
   OpenAPS functies <./Usage/Open-APS-features.md>   
   COB Berekening <./Usage/COB-calculation.rst>
   Gevoeligheidsdetectie <./Configuration/Sensitivity-detection-and-COB.md>
   Profiel wissel <./Usage/Profiles.md>
   Tijdelijk streefdoel <./Usage/temptarget.md>   
   Vertraagde koolhydraten (eCarbs) <./Usage/Extended-Carbs.rst>
   Automatisering <./Usage/Automation.rst>
   Careportal (bestaat niet meer) <./Usage/CPbefore26.rst>
   Open Humans Uploader <./Configuration/OpenHumans.rst>
   Automatisering met andere apps <./Usage/automationwithapp.md>
   Android auto <./Usage/Android-auto.md>  

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Algemene Tips 

   Wisselen van tijdzone <./Usage/Timezone-traveling.md>
   Toegang tot logbestanden <./Usage/Accessing-logfiles.md>
   AccuChek Combo - tips <./Usage/Accu-Chek-Combo-Tips-for-Basic-usage.md> 
   Instellingen exporteren/importeren <./Usage/ExportImportSettings.rst>
   xDrip engineering modus <./Usage/Enabling-Engineering-Mode-in-xDrip.md>

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: AndroidAPS voor kinderen

   Volgen op afstand <./Children/Children.rst>
   SMS Comando's <./Children/SMS-Commands.rst>
   Profielhelper <./Configuration/profilehelper.rst>
   
.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Problemen oplossen

   Problemen oplossen <./Usage/troubleshooting.rst>
   Nightscout Client <../Usage/Troubleshooting-NSClient.md>

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Veelgestelde vragen

   Veelgestelde vragen <./Getting-Started/FAQ.md>

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Veelgebruikte woordenlijst

   Veelgebruikte woordenlijst <./Getting-Started/Glossary.md>

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Waar je hulp kunt vinden 

   Leestips voordat je begint <./Where-To-Go-For-Help/Background-reading.md>
   Contact met anderen <./Where-To-Go-For-Help/Connect-with-other-users.md>
   Documentatie wijzigingen <./Getting-Started/WikiUpdate.rst>

.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Voor zorgprofessionals

   Voor zorgprofessionals <./Resources/clinician-guide-to-AndroidAPS>


.. toctree::
   :maxdepth: 1
   :glob:
   :caption: Hoe je zelf kunt helpen

   Hoe kan je helpen <./Getting-Started/How-can-I-help.md>
   De app of wiki vertalen <./translations.md>
   De wiki verbeteren <./make-a-PR>


.. note:: 
	**Disclaimer en waarschuwing**

	* Alle informatie, gedachten, en de code die hier beschreven staan zijn alleen voor informatieve en educatieve doeleinden. Nightscout probeert zich op geen enkele wijze te houden aan gegevensbewaking van medische gegevens. Gebruik van Nightscout en AndroidAPS is op eigen risico, en gebruik de informatie of code niet om behandelbeslissingen te nemen.

	* Het gebruik van code van github.com is zonder enige garantie of formele ondersteuning. Verdere details zijn te vinden in de licentie, die te vinden is in de Repository op github.

	* Alle product-en bedrijfsnamen, handelsmerken, servicemerken, geregistreerde handelsmerken en geregistreerde dienstmerken zijn eigendom van hun respectievelijke houders. Hun gebruik is voor informatieve doeleinden en impliceert op geen enkele wijze een samenwerking met of goedkeuring van hen.

	Houd er rekening mee dat: - dit project is niet gekoppeld aan en wordt niet ondersteund door: `SOOIL <https://www.sooil.com/eng/>`_, `Dexcom <https://www.dexcom.com/>`_, `Accu-Chek, Roche Diabetes Care <https://www.accu-chek.com/>`_ of `Medtronic <https://www.medtronic.com/>`_
