<h1 align="center">
Transcriptomics analyse van Rheumatoïde Artritis
</h1>

<p align="center">
<strong>Auteur:</strong> Fabian Le Pelvé<br>
<strong>Datum:</strong> 25 Juni 2026
</p>

<hr>

<p align="center">
<img src="images/RA.jpg"
alt="RA Transcriptomics"
width="600"/>
</p>

# Inhoud

- `images/` - zijn de gebruikte figuren voor dit project
- `Data_RA_raw/` - ruwe data van controle groepen e patient groepen
- `script/` - R script
- `referentie genoom/` - is het gebruikte referentie genoom voor dit project
- `bronnen/` - hier zitten de bronnen vermeld zijn in dit project
- `Resultaten/` - hier zitten de excel bestanden met de resultaten


# Transcriptomics

Reumatoïde artritis (RA) is een chronische auto-immuunziekte waarbij het afweersysteem ten onrechte het eigen lichaam aanvalt. Hierdoor ontstaan ontstekingen in de gewrichten, wat kan leiden tot pijn, stijfheid en uiteindelijk gewrichtsschade. Naast de gewrichten kunnen ook andere organen, zoals de longen, het hart en het zenuwstelsel, worden aangetast. Er bestaan verschillende vormen van artritis. Sommige vormen, zoals artrose, gaan niet gepaard met ontstekingen, terwijl andere vormen, waaronder RA, juist worden veroorzaakt door ontstekingsprocessen. Wereldwijd heeft ongeveer 0,3 tot 1% van de bevolking reumatoïde artritis, waarbij vrouwen vaker worden getroffen dan mannen (Smolen et al., 2016).

De exacte oorzaak van RA is nog niet bekend. Onderzoekers verdenken dat de ziekte ontstaat door een combinatie van genetische aanleg, veranderingen in genexpressie, verstoringen van het immuunsysteem en omgevingsfactoren. Omdat de precieze oorzaak nog niet volledig duidelijk is, bestaat er op dit moment geen behandeling die de ziekte volledig kan genezen. Wel kunnen medicijnen de symptomen verminderen en de ziekte afremmen (McInnes & Schett, 2011).
In dit onderzoek werden vier monsters van patiënten met reumatoïde artritis en vier monsters van gezonde personen onderzocht. De monsters waren afkomstig uit het synovium, het slijmvlies van de gewrichten. Met behulp van een transcriptomics-analyse werd gekeken welke genen verschillen in expressie tussen de RA-groep en de controlegroep. Daarnaast werd onderzocht welke biologische processen en pathways hierbij betrokken zijn door middel van een Gene Ontology-analyse (GO). Het doel van dit onderzoek was om meer inzicht te krijgen in de moleculaire processen die een rol spelen bij reumatoïde artritis.

# Methode
Voor dit onderzoek naar reumatoïde artritis (RA) werd RNA-sequencingdata van synoviumbiopten geanalyseerd van vier gezonde controles en vier RA-patiënten met meer dan 12 maanden diagnose. De controlegroep was ACPA-negatief en de RA-groep ACPA-positief. De gebruikte RNA-sequencingdata waren afkomstig van Platzer et al.
De ruwe sequencingbestanden (FASTQ) werden uitgelijnd op het humane referentiegenoom GRCh38.p14 (GCF_000001405.40) met behulp van de align-functie uit het Rsubread-pakket. Hiervoor werd eerst een index van het referentiegenoom aangemaakt. Hierna werden de resulterende BAM-bestanden gesorteerd en geïndexeerd met Rsamtools.
De genexpressie werd gekwantificeerd met featureCounts op basis van het genomic.gtf-annotatiebestand. De differentiële genexpressieanalyse werd uitgevoerd in DESeq2, waarbij een model werd gebruikt op basis van de behandelconditie (RA vs. controle). Significante genen werden geselecteerd bij een aangepaste p-waarde < 0,05 en een |log2FoldChange| > 1.
Vervolgens werd een Gene Ontology-analyse uitgevoerd met clusterProfiler om betrokken biologische processen te identificeren, apart voor verhoogde en verlaagde genen. Resultaten werden visueel weergegeven via ggplot2 en een EnhancedVolcano-plot. Tot slot werd pathway-analyse verricht met behulp van het pathview-pakket op geselecteerde KEGG-pathways. Voor de KEGG-analyse werd specifiek de pathway Rheumatoid arthritis (hsa05323) verder onderzocht.
Voor de analyse werden de volgende R-packages en versies gebruikt: Rsubread (2.20.0), Rsamtools (2.22.0), DESeq2 (1.46.0), clusterProfiler (4.14.6), ggplot2 (4.0.3), EnhancedVolcano (1.24.0), pathview (1.46.0) en KEGGREST (1.46.0).

<p align="center">
<img src="images/RNA_Sequencing_Data.jpg"
alt="Flowdiagram van de transcriptomics-analyse"
width="400"/>
</p>

Flowchart voor beeldgeving van het verloop van het project 


# Resultaten
Om verschillen in genexpressie tussen patiënten met reumatoïde artritis (RA) en gezonde controles te identificeren, werd een differentiële expressieanalyse uitgevoerd met DESeq2. De resultaten werden weergegeven in een volcano plot [Figuur 1]. Hierin zijn genen met een significante verandering in expressie zichtbaar. In totaal werden 4572 differentieel tot expressie gebrachte genen gevonden (padj < 0,05 en |log2FoldChange| > 1). Hiervan waren 2085 genen verhoogd tot expressie gebracht in de RA-groep en 2487 genen verlaagd tot expressie gebracht ten opzichte van de controlegroep. De x-as toont de log2foldchance en de y-as de aangepaste p-waarde -log10padj. Genen met een positieve log2FoldChange zijn verhoogd tot expressie gebracht in de RA-groep en genen met een negatieve log2FoldChange zijn verlaagd tot expressie gebracht.
<p align="center">
<img src="images/RVolcanoPlot_RA.png"
alt="Volcano plot"
width="700"/>
</p>
 
**Figuur 1. Volcano plot van de differentiële genexpressie tussen RA-patiënten en gezonde controles.**
De x-as toont de log2FoldChange en de y-as de aangepaste p-waarde (-log10(padj)). Rode punten geven genen weer die significant differentieel tot expressie komen op basis van padj < 0,05 en |log2FoldChange| > 1.



De GO-analyse werd uitgevoerd op de verhoogd en verlaagd tot expressie gebrachte genen. De 25 belangrijkste GO termen van de verhoogde genen waren voornamelijk gerelateerd aan immuunfuncties, zoals adaptieve immuunrespons, activatie van lymfocyten, B cellen activatie en T cel difirentatie[Figuur 2]. Bij de 25 belangrijkste GO termen van de verlaagde genen waren vooral processen gerelateerd aan celontwikkeling, differentiatie en transcriptregulatie zichtbaar, waaronder spiercel differentiatie, embryonale orgaanontwikkeling en DNA-template transcriptie[Figuur 3]. 
<p align="center">
<img src="images/GO_top25_verhoogd.png"
alt="GO analyse"
width="700"/>
</p>

**Figuur 2. Top 25 GO-termen voor biologische processen van verhoogd tot expressie gebrachte genen.**
De dotplot toont de 25 meest verrijkte biologische processen. De x-as geeft de GeneRatio weer en de grootte van de cirkels geeft het aantal genen (Count) binnen iedere GO-term aan. De kleur van de cirkels geeft de aangepaste p-waarde (p.adjust) weer.
<p align="center">
<img src="images/GO_top25_verlaagd.png"
alt="GO analyse"
width="700"/>
</p>

**Figuur 3. Top 25 GO-termen voor biologische processen van verlaagd tot expressie gebrachte genen.**
De dotplot toont de 25 meest verrijkte biologische processen. De x-as geeft de GeneRatio weer en de grootte van de cirkels geeft het aantal genen (Count) binnen iedere GO-term aan. De kleur van de cirkels geeft de aangepaste p-waarde (p.adjust) weer.

Ten slotte werd het KEGG-pathway Rheumatoid arthritis (hsa05323) onderzocht met Pathview [Figuur 4]. In dit pathway zijn genen weergegeven die betrokken zijn bij verschillende processen die een rol spelen bij RA. De genen zijn op basis van hun expressieverandering gekleurd, waardoor zichtbaar wordt welke genen verhoogd of verlaagd tot expressie komen. De pathway bevat onder andere onderdelen die betrokken zijn bij immuunreacties en ontstekingsprocessen. Hierdoor geeft de analyse een overzicht van hoe de gevonden genexpressieveranderingen samenhangen met processen die betrokken zijn bij RA.
</p>

<p align="center">
<img src="images/hsa05323.pathview.png"
alt="KEGG Pathway analyse"
width="700"/>
</p>

**Figuur 4. KEGG-pathway Rheumatoid arthritis (hsa05323) weergegeven met Pathview.**
De afbeelding toont de verschillende genen en biologische onderdelen binnen het Rheumatoid arthritis-pathway. De kleur van de genen geeft de verandering in genexpressie tussen de RA-groep en de controlegroep weer.

# Conclusie
In dit onderzoek werd transcriptomics gebruikt om verschillen in genexpressie tussen RA-patiënten en gezonde controles te onderzoeken. De analyse identificeerde 4572 significant veranderde genen, waarvan zowel verhoogde als verlaagde expressie werd waargenomen. Deze resultaten tonen aan dat reumatoïde artritis gepaard gaat met grootschalige veranderingen in genregulatie binnen synoviumweefsel.
De GO-analyse liet zien dat veel van de differentieel tot expressie gebrachte genen betrokken zijn bij immuunprocessen, waaronder activatie van lymfocyten en regulatie van ontstekingsreacties. Dit ondersteunt de huidige kennis dat RA een auto-immuunziekte is waarbij een ontregelde immuunrespons een centrale rol speelt. De KEGG-analyse bevestigde deze bevindingen doordat verschillende genen binnen het bekende RA-pathway (hsa05323) afwijkende expressie vertoonden.
Een beperking van dit onderzoek is de relatief kleine steekproefomvang van vier patiënten en vier controles. Hierdoor kunnen individuele verschillen een relatief grote invloed hebben op de resultaten. Een vervolgonderzoek zou gebruik kunnen maken van grotere steekproefomvang en meerdere analyses om de rol van specifieke genen verder te onderzoeken. Desondanks geven de resultaten waardevol inzicht in de moleculaire mechanismen die bijdragen aan het ontstaan van reumatoïde artritis.

# Kennis over github
Voor dit project is gebruikgemaakt van GitHub om alle bestanden centraal op te slaan en het project overzichtelijk te organiseren. Op de GitHub-repository zijn de gebruikte data, scripts en resultaten opgeslagen, waardoor alle onderdelen van het onderzoek eenvoudig terug te vinden zijn. Daarnaast maakt GitHub gebruik van branches, waarmee verschillende versies van bestanden afzonderlijk kunnen worden beheerd. Hierdoor konden wijzigingen tijdens de analyse worden bijgehouden en getest zonder dat eerdere versies verloren gingen.

# inrichting van github
De GitHub-repository is overzichtelijk ingedeeld in verschillende bestanden en mappen. Er zijn afzonderlijke bestanden opgenomen voor het gebruikte R-script, de bronnen en het referentiegenoom. De ruwe data zijn opgeslagen in een aparte map, waarin alle relevante datasets zijn verwerkt. Daarnaast bevat de map Images de figuren die tijdens het project zijn gegenereerd. In het README-bestand wordt het volledige project beschreven, inclusief de structuur van de repository en de gebruikte bestanden.

# Beheersysteem 
In dit onderzoek is GitHub gebruikt als centrale plek om alle bestanden op te slaan, zodat alles makkelijk terug te vinden is. Daarnaast is het platform gebruikt om het project te documenteren en duidelijk te maken welke stappen zijn uitgevoerd. Bij het inrichten van de GitHub is gekozen voor een overzichtelijke scheiding tussen de resultaten, data, afbeeldingen en scripts. Hierdoor kunnen de verschillende onderdelen makkelijker worden teruggevonden en wordt verwarring voorkomen.
In de map Data_RA_raw staat de gebruikte ruwe data die voor de analyse is gebruikt. In de map scripts staat het gebruikte R-script voor dit project, waarin alle stappen van de analyses zijn genoteerd. In de map referentie_genoom staat informatie over het gebruikte referentiegenoom. In de map resultaten bevinden zich de resultaten van de uitgevoerde analyses, zoals de countmatrix, GO-analyse en DESeq2-analyse. In de map images staan alle gebruikte afbeeldingen. In de map bronnen staan de gebruikte bronnen voor dit verslag opgeslagen. Het bestand README.md wordt gebruikt om het project toe te lichten.
Door deze inrichting is het gemakkelijker om te zien welke data, scripts en resultaten bij elkaar horen. Hierdoor blijft het project overzichtelijk en kunnen de uitgevoerde analyses en resultaten gemakkelijker worden teruggevonden en gereproduceerd.

