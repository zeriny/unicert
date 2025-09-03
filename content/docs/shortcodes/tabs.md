---
bookHidden: true
---


# Tabs

Tabs let you organize content by context, for example installation instructions for each supported platform.

```tpl
{{</* tabs "id" */>}}
{{%/* tab "MacOS" */%}} # MacOS Content {{%/* /tab */%}}
{{%/* tab "Linux" */%}} # Linux Content {{%/* /tab */%}}
{{%/* tab "Windows" */%}} # Windows Content {{%/* /tab */%}}
{{</* /tabs */>}}
```

## Example

{{< tabs >}}

{{% tab "MacOS" %}}
# MacOS

This is tab **MacOS** content.

Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
protulit, sed sed aere valvis inhaesuro Pallas animam: qui _quid_, ignes.
Miseratus fonte Ditis conubia.
{{% /tab %}}

{{% tab "Linux" %}}
# Linux

This is tab **Linux** content.

Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
protulit, sed sed aere valvis inhaesuro Pallas animam: qui _quid_, ignes.
Miseratus fonte Ditis conubia.
{{% /tab %}}

{{% tab "Windows" %}}
# Windows

This is tab **Windows** content.

Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
protulit, sed sed aere valvis inhaesuro Pallas animam: qui _quid_, ignes.
Miseratus fonte Ditis conubia.
{{% /tab %}}

{{< /tabs >}}

# Hints

Hint shortcode can be used as a hint/alert/notification block.



## Support for markdown alerts

> [!NOTE]
> **Note**  
> Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
> stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa

> [!TIP]
> **Tip**  
> Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
> stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa

> [!IMPORTANT]
> **Important**  
> Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
> stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa

> [!WARNING]
> **Warning**  
> Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
> stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa

> [!CAUTION]
> **Caution**  
> Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
> stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa


# Buttons

Buttons are styled links that can lead to local page or external link.

## Example

```tpl
{{</* button relref="/" [class="..."] */>}}Get Home{{</* /button */>}}
{{</* button href="https://github.com/alex-shpak/hugo-book" */>}}Contribute{{</* /button */>}}
```

{{<button relref="/">}}Get Home{{</button>}}
{{<button href="https://github.com/alex-shpak/hugo-book">}}Contribute{{</button>}}

# Badges

{{< badge title="Title" value="Value" >}}
{{< badge style="info" title="Hugo" value="0.147.6" >}}
{{< badge style="success" title="Build" value="Passing" >}}
{{< badge style="warning" title="Coverage" value="25%" >}}
{{< badge style="danger" title="Issues" value="120" >}}

Badges can be used to annotate your pages with additional information or mark specific places in markdown content.

## Examples

| Shortcode | Output |
| --        | --     |
| `{{</* badge style="info" title="hugo" value="0.147.6" */>}}`     | {{< badge style="info" title="Hugo" value="0.147.6" >}}     |
| `{{</* badge style="success" title="Build" value="Passing" */>}}` | {{< badge style="success" title="Build" value="Passing" >}} |
| `{{</* badge style="warning" title="Coverage" value="25%" */>}}`  | {{< badge style="warning" title="Coverage" value="25%" >}}  |
| `{{</* badge style="danger" title="Issues" value="120" */>}}`     | {{< badge style="danger" title="Issues" value="120" >}}     |
| | |
| `{{</* badge style="info" title="Title" */>}}`                    | {{< badge style="info" title="Title" >}}                    |
| `{{</* badge style="info" value="Value" */>}}`                    | {{< badge style="info" value="Value" >}}                    |
| `{{</* badge title="Default" */>}}`                               | {{< badge value="Default" >}}                               |

## Use in links 

A badge can be wrapped in markdown link producing following result: [{{< badge title="Hugo" value="0.147.6" >}}](https://github.com/gohugoio/hugo/releases/tag/v0.147.6)
```tpl
[{{</* badge title="Hugo" value="0.147.6" */>}}](https://github.com/gohugoio/hugo/releases/tag/v0.147.6)
```
