# Module-IFrame

Embed an external web page, or your own HTML, in an Edrys class. Use it to put an existing tool, simulator,
documentation page or video into a lab without writing a module. It is shown in every room (`show-in: *`) and has
no shared state: every peer loads the page from the module configuration.

## Usage

Add the module to your class with this URL:

```
https://edrys-labs.github.io/module-iframe/index.html
```

## Configuration

Open the module in the class settings. Each of the four tabs has two fields:

- **src**: the URL of the page to embed.
- **srcdoc**: HTML to show instead. It is only used when `src` is empty.

| Tab | Shown to |
|-----|----------|
| General (`config`) | everyone |
| Teacher (`teacherConfig`) | teachers |
| Student (`studentConfig`) | students |
| Station (`stationConfig`) | stations |

A role tab that sets `src` or `srcdoc` **replaces** the general tab for that role, for example to show students
an exercise and teachers the solution. Empty role tabs fall back to the general tab. Changes are shown to everyone
as soon as the settings are saved. Without any page configured, the module says what to set.

If you edit the class configuration as YAML instead:

```yaml
config:
  src: https://example.com/exercise
teacherConfig:
  src: https://example.com/solution
```

or, with inline HTML (use a literal block `|` so line breaks are kept):

```yaml
config:
  srcdoc: |
    <h1>Task 1</h1>
    <p>Open the simulator in the next tab and build the circuit.</p>
```

## Things to know

- **Not every site can be embedded.** Many sites (Google, GitHub, most learning platforms) forbid being shown in a
  frame (`X-Frame-Options` / `frame-ancestors`). The browser then shows an empty or "refused to connect" frame.
  This is not a bug in the module; check whether the site offers an embed URL (e.g. YouTube's
  `https://www.youtube.com/embed/<id>`).
- **Permissions.** The embedded page gets the same permissions Edrys gives modules: fullscreen, camera,
  microphone, Web Serial, MIDI, clipboard and others. Browsers still ask the user before using camera,
  microphone or serial devices.
- **`srcdoc` HTML has the module's access to Edrys.** Scripts in `srcdoc` run with the module's origin, so they
  can reach the module and through it Edrys (send messages, change the room's shared state). Only paste HTML you
  trust.

## License

[MIT](LICENSE) © edrys-labs
