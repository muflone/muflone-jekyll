# {{ site.data.translations[page.language].downloads.distributions.title }}

{{ site.data.translations[page.language].downloads.distributions.text1 | replace: '$(NAME)', site.data[page.product].name }}

{{ site.data.translations[page.language].downloads.distributions.text2 | replace: '$(GITHUB)', site.data[page.product].gitrepo }}

# {{ site.data.translations[page.language].downloads.packages.title }}

{{ site.data.translations[page.language].downloads.packages.text1 }}

<script>
  $(document).ready(function(){
    $.ionTabs("#tabs_packages");
  });
</script>
<div class="ionTabs" id="tabs_packages" data-name="Tabs_Group_name">
    <ul class="ionTabs__head">
{% for version in site.data[page.product].versions %}
        <li class="ionTabs__tab" data-target="Tab_{{ version.normalized }}">{{ version.version }}</li>
{% endfor %}
    </ul>
    <div class="ionTabs__body">
{% for version in site.data[page.product].versions %}
        <div class="ionTabs__item" data-name="Tab_{{ version.normalized }}">
          <table id="packages">
            <thead>
              <tr>
                <th>{{ site.data.translations[page.language].downloads.packages.type }}</th>
                <th>{{ site.data.translations[page.language].downloads.packages.name }}</th>
                <th>{{ site.data.translations[page.language].downloads.packages.size }}</th>
                <th>{{ site.data.translations[page.language].downloads.packages.md5 }}</th>
                <th>{{ site.data.translations[page.language].downloads.packages.action }}</th>
              </tr>
            </thead>
  {% for package in version.packages %}
            <tr>
              <td class="type">
                <img src="/theme/images/{{ site.data.translations[page.language].downloads.types[package.type].icon }}">
                {{ site.data.translations[page.language].downloads.types[package.type].title }}
              </td>
              <td class="name">{{ package.filename }}</td>
              <td class="size">{{ package.size }}</td>
              <td class="md5sum">{{ package.md5sum | upcase }}</td>
              <td>
    {% if package.type != 'aur' %}
                <a href="/resources/{{ page.product }}/archive/{{ version.version}}/{{ package.filename }}"
                  title="{{ site.data.translations[page.language].downloads.from.muflone }}">
                  <img src="/theme/images/muflone-32.png"></a>
                <a href="{{ site.data[page.product].gitrepo }}/releases/download/{{ version.version }}/{{ package.filename }}"
                  title="{{ site.data.translations[page.language].downloads.from.github }}">
                  <img src="/theme/images/github-32.png"></a>
    {% else %}
                <a href="https://aur.archlinux.org/packages/{{ package.filename }}/"
                  title="{{ site.data.translations[page.language].downloads.from.aur }}"
                  target="_blank">
                  <img src="/theme/images/archlinux-32.png"></a>
    {% endif %}
              </td>
            </tr>
  {% endfor %}
          </table>
        </div>
{% endfor %}
        <div class="ionTabs__preloader"></div>
    </div>
</div>