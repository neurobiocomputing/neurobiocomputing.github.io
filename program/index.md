---
title: Program
description: Conference dates and program updates for NeuroBiological Computing 2027.
---

<p class="lead">Three days exploring biological computation.</p>

NeuroBiological Computing 2027 takes place on **{{ site.event.date_label }}**. The scientific program and session times will be announced here.

<div class="table-responsive my-4">
  <table class="table align-middle">
    <caption>Confirmed conference dates. Sessions and times are to be announced.</caption>
    <thead><tr><th scope="col">Day</th><th scope="col">Date</th><th scope="col">Program</th></tr></thead>
    <tbody>
      {% for day in site.data.program.days %}
      <tr><th scope="row">{{ day.name }}</th><td><time datetime="{{ day.date }}">{{ day.date | date: "%d %B %Y" }}</time></td><td>To be announced</td></tr>
      {% endfor %}
    </tbody>
  </table>
</div>

<a class="btn btn-primary" href="{{ site.event.calendar | relative_url }}" download>Add the conference to your calendar</a>
