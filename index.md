---
layout: default
---

# Getting Started

[Helm](https://helm.sh/) must be installed to use the charts. Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

Once Helm is set up properly, add the repo as follows:

```console
$ helm repo add {{ site.repo_name }} {{ site.url }}
```

You can then run `helm search repo {{ site.repo_name }}` to see the charts.

# Charts

{% for helm_chart in site.data.index.entries %}
{% assign title = helm_chart[0] | capitalize %}
{% assign all_charts = helm_chart[1] | sort: 'created' | reverse %}
{% assign latest_chart = all_charts[0] %}

<h3>
  {% if latest_chart.icon %}
  <img src="{{ latest_chart.icon }}" style="height:1.2em;vertical-align: text-top;" />
  {% endif %}
  {{ title }}
</h3>

[Home]({{ latest_chart.home }}) \| [Source]({{ latest_chart.sources[0] }})

{{ latest_chart.description }}

```console
$ helm install {{ site.repo_name }}/{{ latest_chart.name }} --name myrelease --version {{ latest_chart.version }}
```

| Chart Version | App Version | Date |
|---------------|-------------|------|
{% for chart in all_charts -%}
{% unless chart.version contains "-" -%}
| [{{ chart.name }}-{{ chart.version }}]({{ chart.urls[0] }}) | {{ chart.appVersion }} | {{ chart.created | date_to_rfc822 }} |
{% endunless -%}
{% endfor -%}

{% endfor %}

# Project Background

[dNationCloud](https://github.com/dNationCloud) Helm Hub project is maintained and used in production by [dNation](https://www.dnation.tech/) professionals 
to simplify their day-to-day tasks.
