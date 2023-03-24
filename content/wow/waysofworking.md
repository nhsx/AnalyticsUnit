---
layout: base
title: DART Innovation Branch - Ways of Working
permalink: waysofworking.html
---
 
<h2> {{page.title}} </h2>
 
 
 <div class="nhsuk-expander-group">
  <details class="nhsuk-details nhsuk-expander">
    <summary class="nhsuk-details__summary">
      <span class="nhsuk-details__summary-text">
        Reproducible Analytical Pipelines (RAP)
      </span>
    </summary>
    <div class="nhsuk-details__text">
      <p><a href="https://nhsdigital.github.io/rap-community-of-practice/">Reproducible Analytical Pipelines (RAP)</a> are becoming the standard for creating analytical outputs in government; combining a number of ways of working that help to improve the reliability, transparency, and speed of statistics publications. Recently the <a href="https://www.gov.uk/government/publications/better-broader-safer-using-health-data-for-research-and-analysis">Goldacre Review</a> identified RAP as the essential element to ensure high-quality analysis. </p>
      <p>Both our internal and external work constantly has one eye on how to increase the level of RAP and support reuse of our work.</p>

    </div>
  </details>

  <details class="nhsuk-details nhsuk-expander">
    <summary class="nhsuk-details__summary">
      <span class="nhsuk-details__summary-text">
        Code First (mostly Python, R)
      </span>
    </summary>
    <div class="nhsuk-details__text">
      <p>Whilst most of our work is python based we aim to use and support a wider variety of languages recognising that no single language can currently, or will continue indefinitely, to be optimal for every task.</p>
      <p>For new members of the team looking at learning Python and R we recommend starting with:
      <ul>
        <li> Python -  see <a href="https://nhs-pycom.net/resources">nhs-pycom.net/resources</a> and wider website as a start.  Engage with the nhs-pycom slack (link on the website) as a secondary point to see what the wider community recommends.   You can also see our peer-to-peer internal training <a href="https://github.com/nhs-pycom/coding-club">here</a>.</li>
        <li> R - see <a href="https://nhsrcommunity.com/events/">nhsrcommunity.com</a> as a start.  Engage with the NHSR slack (link on website).</li>
      </ul>      
      </p>
    </div>
  </details>

  <details class="nhsuk-details nhsuk-expander">
    <summary class="nhsuk-details__summary">
      <span class="nhsuk-details__summary-text">
        Levels of code output
      </span>
    </summary>
    <div class="nhsuk-details__text">
      <p>We have three levels of code (depending on the envisaged end use-case):</p>
      <ul>
        <li>  Prototypes - these pieces of code are delivered as working examples of a method or tool set but then not continually maintained.  Their main purpose is to backup the technical report with shared code and clear examples.</li>
        <li> Standalone - these pieces of code are designed for reuse by a developer/analyst.  They will need tweaking for the local situation and should only be applied with domain/data specific knowledge to ensure they are not misused.  These pieces would be used by any ICS/trust project as a suite of possible starting points to apply a range of data science techniques.  These code bases need a code owner to monitor their status and ensure they remain active and updated over time.</li>
        <li> Integrated - these pieces of code have an eventual aim to turn into a tool that can be integrated alongside NHS England infrastructure and data to create new capabilities for our analysts.  These will need maintenance to keep them active but more importantly a full software engineering cycle including requirements, full refactor to reach an Alpha point and then a full testing programme to move through Beta and into release.   This is beyond the current capabilities of the team and so requires support from DMIS or additional resourcing. </li>
      </ul>
    <p>These rough definitions help us to prioritise code development and ask ourselves when do we need to care about maintaining and pushing best practice on a code and when can we just ensure the code has reached a stable state we can come back to at a later date.</p>

    </div>
  </details>

  <details class="nhsuk-details nhsuk-expander">
    <summary class="nhsuk-details__summary">
      <span class="nhsuk-details__summary-text">
        Github
      </span>
    </summary>
    <div class="nhsuk-details__text">
      <p>We use github as our main collaboration tool when the code is not sensitive.  To support our work in github we use a <a href="https://github.com/nhsx/analyticsunit-template">standard project template</a> with branches of this template including a more detailed <a href="https://github.com/nhsx/analyticsunit-template/tree/cookiestructure">cookiestructure</a>, <a href="https://github.com/nhsx/analyticsunit-template/tree/hooks">hooks</a> for simple code quality checks, <a href="https://github.com/nhsx/analyticsunit-template/tree/tests">tests</a>, MkDocs documentation, and docker setup.</p>
      <p>These templates and branches are aimed at supporting gradual development of the codebase towards higher RAP standards as demonstrated by this example flow
        <img class="nhsuk-card__img" src="assets/img/codefeatures.png" alt="Branches of our project template" width="800"/>
      </p>  
    </div>
  </details>

  <details class="nhsuk-details nhsuk-expander">
    <summary class="nhsuk-details__summary">
      <span class="nhsuk-details__summary-text">
        Open Working
      </span>
    </summary>
    <div class="nhsuk-details__text">
      <p>We champion open ways of working.  At the 2022 NHS-R Conference Jonny spoke on <a href="https://github.com/nhs-r-community/conference-2022/blob/main/talks/2022-11-16/16_Nov%20Jonny%20Pearson%20-NHSRconf22_SharingInTheOpen2.pdf">sharing in the open</a>. Much of our thinking follows the GDS blogs and <a href="https://www.annashipman.co.uk/jfdi/open-code-resources.html">Anna Shipman's open code resources</a>.</p>
      <p>We've also set out our thinking behind the mandate and approach of sharing code in the open in our <a href="https://nhsx.github.io/AnalyticsUnit/codeintheopen.html">thinking section</a></p>
      <p>We also have published and use a <a href="https://github.com/nhsengland/analyticsunit-template/blob/main/OPEN_CODE_CHECKLIST.md​">open code checklist</a> as a starting point to support making our code open with a series of appropriate checks.</p>

    </div>
  </details>

</div>