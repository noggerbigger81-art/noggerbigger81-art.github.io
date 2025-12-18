# Create a Warrior Cats–style wiki website with separate HTML pages for characters, places, religions, and events.
# The site will be packaged into a zip for easy download.

import os, zipfile, textwrap, json, pathlib

base_dir = "/mnt/data/rebirth_wiki"
os.makedirs(base_dir, exist_ok=True)

def write(path, content):
    os.makedirs(os.path.dirname(path), exist_ok=True)
    with open(path, "w", encoding="utf-8") as f:
        f.write(content)

# Basic CSS
css = """
body {
  font-family: Georgia, "Times New Roman", serif;
  background:#111;
  color:#eee;
  margin:0;
}
header {
  background:#2a2a2a;
  padding:16px 24px;
  border-bottom:2px solid #444;
}
header h1 { margin:0; }
nav a {
  color:#ffd966;
  margin-right:16px;
  text-decoration:none;
}
nav a:hover { text-decoration:underline; }
.container {
  display:flex;
}
.sidebar {
  width:260px;
  background:#1a1a1a;
  padding:16px;
  border-right:1px solid #333;
}
.sidebar h3 {
  color:#ffd966;
  margin-top:0;
}
.sidebar a {
  display:block;
  color:#ccc;
  margin:6px 0;
  text-decoration:none;
}
.sidebar a:hover { color:#fff; }
.content {
  padding:24px;
  max-width:900px;
}
.infobox {
  float:right;
  width:260px;
  background:#1c1c1c;
  border:1px solid #333;
  padding:12px;
  margin:0 0 16px 16px;
}
.infobox h3 {
  margin-top:0;
  color:#ffd966;
}
.section h2 {
  border-bottom:1px solid #444;
  padding-bottom:4px;
  color:#ffd966;
}
footer {
  clear:both;
  padding:16px;
  background:#2a2a2a;
  border-top:2px solid #444;
  margin-top:24px;
  text-align:center;
  font-size:0.9em;
  color:#aaa;
}
"""

write(f"{base_dir}/style.css", css)

# Base HTML template
def page(title, sidebar_links, body):
    links_html = "\n".join([f'<a href="{href}">{name}</a>' for name, href in sidebar_links])
    return f"""<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>{title}</title>
<link rel="stylesheet" href="../style.css">
</head>
<body>
<header>
  <h1>Rebirth? Wiki</h1>
  <nav>
    <a href="../index.html">Home</a>
    <a href="../characters/index.html">Characters</a>
    <a href="../places/index.html">Places</a>
    <a href="../religions/index.html">Religions</a>
    <a href="../events/index.html">Events</a>
  </nav>
</header>
<div class="container">
  <aside class="sidebar">
    <h3>Navigation</h3>
    {links_html}
  </aside>
  <main class="content">
    {body}
  </main>
</div>
<footer>
  Fan-made Warrior Cats–style wiki for <em>Twelve: AU</em> and <em>Rebirth?</em>
</footer>
</body>
</html>
"""

# Index
write(f"{base_dir}/index.html", """<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Rebirth? Wiki</title>
<link rel="stylesheet" href="style.css">
</head>
<body>
<header>
  <h1>Rebirth? Wiki</h1>
  <nav>
    <a href="characters/index.html">Characters</a>
    <a href="places/index.html">Places</a>
    <a href="religions/index.html">Religions</a>
    <a href="events/index.html">Events</a>
  </nav>
</header>
<div class="content">
  <p>This wiki documents the characters, places, religions, and events of <strong>Twelve: AU</strong> and <strong>Rebirth?</strong>.
  Pages expand on personalities, appearances, histories, and story outcomes based on the provided text and character profiles.</p>
  <p><strong>Content Warning:</strong> Child neglect, death, grief, suicide, manipulative relationships, and heavy religious themes.</p>
</div>
<footer>Fan-made wiki</footer>
</body>
</html>
""")

# Characters index
characters = [
    ("Imperia (Imp)", "imperia.html"),
    ("May", "may.html"),
    ("Simon", "simon.html"),
    ("Devo", "devo.html"),
    ("Kate", "kate.html"),
    ("Princess", "princess.html"),
    ("Biscuits", "biscuits.html"),
]

char_links = [(name, file) for name, file in characters]

write(f"{base_dir}/characters/index.html",
      page("Characters", char_links,
           "<h2>Characters</h2><p>Major and minor characters in the story.</p>"))

# Helper to build character pages
def character_page(name, infobox_items, sections):
    infobox_html = "<div class='infobox'><h3>{}</h3>{}</div>".format(
        name,
        "".join([f"<p><strong>{k}:</strong> {v}</p>" for k, v in infobox_items])
    )
    sections_html = "".join([f"<div class='section'><h2>{title}</h2><p>{content}</p></div>" for title, content in sections])
    return infobox_html + sections_html

# Imperia page
imp_body = character_page(
    "Imperia",
    [
        ("Aliases", "Imp, Old Man, Unc, Demon Guy"),
        ("Gender", "Male"),
        ("Species", "Reaper (Feline)"),
        ("Status", "Alive (formerly deceased as a mortal)"),
        ("Religion", "Atheist; formerly Skankian"),
        ("Ability", "Metaphysical Foresight"),
    ],
    [
        ("History",
         "Imperia was once a mortal feline who died by accidental drowning during a sea storm. "
         "After death, he became a reaper and later violated reaper code by releasing and reviving souls. "
         "As punishment, he was imprisoned in the Void, bound to a pocket watch, until May freed him."),
        ("Personality",
         "Imp is deeply morally ambiguous. Charming, laidback, and often funny, he presents himself as a cool, protective uncle figure. "
         "Beneath this lies a manipulative streak: he withholds information, lies 'for protection,' and justifies harmful actions as necessary. "
         "He genuinely cares for May and her circle, yet repeatedly prioritizes his own judgment over their autonomy."),
        ("Appearance",
         "Imperia has deep crimson fur marked with darker spots, tall black-tipped ears, and golden eyes that glow faintly in darkness. "
         "His reaper forms include shadowy bat-like wings, a long segmented bone tail, and a smaller impish shape with oversized ears."),
        ("Story",
         "A main character in Parts 1 and 2 and the anti-hero of Part 3, Imp’s arc centers on control, guilt, and grief. "
         "His search for Ollie and his murder of Biscuits reveal his willingness to cross any line, even as he insists he is doing what is right.")
    ]
)

write(f"{base_dir}/characters/imperia.html", page("Imperia", char_links, imp_body))

# May page
may_body = character_page(
    "May",
    [
        ("Gender", "Female"),
        ("Species", "Feline (Ragamuffin Tabby mix)"),
        ("Status", "Alive (formerly deceased; revived)"),
        ("Religion", "Nandian; formerly Estandian"),
        ("Ability", "Guardian Angel; possession (via Imp)"),
    ],
    [
        ("History",
         "May was struck by lightning during a game of hide and seek and died, awakening in the Void where she met Imperia. "
         "By freeing him, she was revived and tasked with helping lost souls and vessels."),
        ("Personality",
         "Emotionally intelligent and deeply empathetic, May thrives on social connection. "
         "Her greatest flaw is trust: she believes in the good of those close to her, even when faced with clear red flags. "
         "This makes her especially vulnerable to Imp’s manipulation."),
        ("Appearance",
         "May has soft peach-cream fur, a fluffy chest and face, large rosy inner ears, and bright golden eyes. "
         "A star-shaped birthmark rests beneath her right eye, and her thick tail alternates between creamy white and caramel."),
        ("Story",
         "Across all parts, May acts as a moral and emotional anchor. "
         "She helps multiple souls find peace, survives repeated brushes with death, and struggles to reconcile her kindness "
         "with the unsettling truths of the afterlife.")
    ]
)

write(f"{base_dir}/characters/may.html", page("May", char_links, may_body))

# Simon page
simon_body = character_page(
    "Simon",
    [
        ("Gender", "Male"),
        ("Species", "Feline (Bengal Tabby)"),
        ("Status", "Deceased"),
        ("Religion", "Atheist; formerly Landian"),
        ("Residence", "Shadowy Fireforest"),
    ],
    [
        ("History",
         "Simon lived with his brother Devo until their mother abandoned them. "
         "The arrival of Princess and the death of Ollie marked the beginning of his downward spiral."),
        ("Personality",
         "Quiet, introspective, and increasingly bitter, Simon is a good cat crushed by grief and disillusionment. "
         "He judges silently, loves deeply, and turns his anger inward. "
         "His loss of faith leaves him unmoored and vulnerable."),
        ("Appearance",
         "Simon has sandy-brown fur with a darker saddle marking, a cream underbelly, and striking blue eyes. "
         "His build is lithe with a bushy, curved tail and a soft scruff around his neck."),
        ("Story",
         "The protagonist of Part 1 and antagonist of Part 2, Simon ultimately dies by suicide. "
         "He is sent to the Shadowy Fireforest, accepting his fate in a quiet, devastating conclusion.")
    ]
)

write(f"{base_dir}/characters/simon.html", page("Simon", char_links, simon_body))

# Devo page
devo_body = character_page(
    "Devo",
    [
        ("Gender", "Male"),
        ("Species", "Feline (Bengal Tabby)"),
        ("Status", "Alive"),
        ("Religion", "Landian"),
    ],
    [
        ("History",
         "Devo grew up alongside Simon and later welcomed Princess with open arms, "
         "unaware of how deeply this would fracture his relationship with his brother."),
        ("Personality",
         "Optimistic, affectionate, and earnest, Devo wears his heart openly. "
         "He longs for connection and struggles to understand Simon’s rejection."),
        ("Appearance",
         "Devo’s fur ranges from cocoa to chestnut, with fluffy cheeks, a plume-like tail, and large pink-inner ears. "
         "His grey eyes and cheerful grin give him an approachable warmth."),
        ("Story",
         "Throughout Part 2, Devo becomes an emotional bridge between characters, "
         "grieving Simon while still trying to protect Princess and move forward.")
    ]
)

write(f"{base_dir}/characters/devo.html", page("Devo", char_links, devo_body))

# Kate page
kate_body = character_page(
    "Kate",
    [
        ("Gender", "Female"),
        ("Species", "Feline (Siberian mix)"),
        ("Status", "Alive"),
        ("Religion", "Nandian; formerly Landian"),
    ],
    [
        ("History",
         "Kate lived closely with her younger brother Ollie until his sudden death. "
         "Her grief becomes a defining force in Part 1."),
        ("Personality",
         "Quiet and observant at first, Kate grows into a more vocal and proactive presence. "
         "She is compassionate, resilient, and capable of enduring immense loss without losing herself."),
        ("Appearance",
         "Kate has a plump, fluffy build, warm brown fur with darker spots, and a bright red collar with a golden bell. "
         "Her bushy tail curls slightly at the tip, reinforcing her cozy, friendly presence."),
        ("Story",
         "As the protagonist of Part 1, Kate’s arc focuses on mourning and acceptance. "
         "Imp’s promise that she will reunite with Ollie provides bittersweet closure.")
    ]
)

write(f"{base_dir}/characters/kate.html", page("Kate", char_links, kate_body))

# Princess page
princess_body = character_page(
    "Princess",
    [
        ("Gender", "Female"),
        ("Species", "Feline (Bengal Tabby)"),
        ("Status", "Alive"),
        ("Religion", "Atheist"),
    ],
    [
        ("History",
         "Princess was dropped into Simon and Devo’s life by their parents, unwanted and unexpected."),
        ("Personality",
         "Innocent and trusting, Princess seeks affection and stability. "
         "Her very existence becomes a source of conflict despite her lack of malice."),
        ("Appearance",
         "A smaller Bengal tabby with soft markings and youthful features that emphasize her vulnerability."),
        ("Story",
         "Princess survives Part 2 as a quiet reminder of unresolved family trauma, "
         "largely shielded from the full truth of Simon’s fate.")
    ]
)

write(f"{base_dir}/characters/princess.html", page("Princess", char_links, princess_body))

# Biscuits page
biscuits_body = character_page(
    "Biscuits",
    [
        ("Gender", "Male"),
        ("Species", "Reaper (Feline)"),
        ("Status", "Faded"),
        ("Ability", "Metaphysical Foresight"),
    ],
    [
        ("History",
         "Biscuits was a reaper who died as a mortal in a car accident and later served in the Rift."),
        ("Personality",
         "Little is known, though his conflict with Imp suggests ideological or personal tension."),
        ("Appearance",
         "As a reaper, Biscuits shared traits common to Rift-dwellers, marked by otherworldly features."),
        ("Story",
         "Biscuits is murdered by Imp, becoming a symbol of how far Imp is willing to go to protect himself and his secrets.")
    ]
)

write(f"{base_dir}/characters/biscuits.html", page("Biscuits", char_links, biscuits_body))

# Places index and pages
places = [("Earth", "earth.html"), ("The Void", "void.html"), ("The Rift", "rift.html"), ("Shadowy Fireforest", "fireforest.html")]
place_links = [(n, f) for n, f in places]

write(f"{base_dir}/places/index.html", page("Places", place_links, "<h2>Places</h2>"))

write(f"{base_dir}/places/earth.html", page("Earth", place_links, "<h2>Earth</h2><p>The mortal world where living cats reside, mirroring the real world.</p>"))
write(f"{base_dir}/places/void.html", page("The Void", place_links, "<h2>The Void</h2><p>A white, timeless space where souls are bound or imprisoned, linked to reaper artifacts.</p>"))
write(f"{base_dir}/places/rift.html", page("The Rift", place_links, "<h2>The Rift</h2><p>The realm of reapers, governed by strict code and punishment.</p>"))
write(f"{base_dir}/places/fireforest.html", page("Shadowy Fireforest", place_links, "<h2>Shadowy Fireforest</h2><p>The Landian hell, where Simon is ultimately sent.</p>"))

# Religions
religions = [("Landina", "landina.html"), ("Nandina", "nandina.html"), ("Estandina", "estandina.html"), ("Skankian", "skankian.html")]
relig_links = [(n, f) for n, f in religions]

write(f"{base_dir}/religions/index.html", page("Religions", relig_links, "<h2>Religions</h2>"))

write(f"{base_dir}/religions/landina.html", page("Landina", relig_links, "<h2>Landina</h2><p>Faith in the Stars, guaranteed peace unless forbidden.</p>"))
write(f"{base_dir}/religions/nandina.html", page("Nandina", relig_links, "<h2>Nandina</h2><p>A stricter branch of Landina requiring earned virtue.</p>"))
write(f"{base_dir}/religions/estandina.html", page("Estandina", relig_links, "<h2>Estandina</h2><p>Moon-guided faith with purgatorial punishment.</p>"))
write(f"{base_dir}/religions/skankian.html", page("Skankian", relig_links, "<h2>Skankian</h2><p>An older belief system abandoned by Imp after becoming a reaper.</p>"))

# Events
events = [("Kate’s Story", "kate_story.html"), ("Simon’s Story", "simon_story.html"), ("Imp’s Story", "imp_story.html")]
event_links = [(n, f) for n, f in events]

write(f"{base_dir}/events/index.html", page("Events", event_links, "<h2>Events</h2>"))

write(f"{base_dir}/events/kate_story.html", page("Kate’s Story", event_links, "<h2>Kate’s Story</h2><p>Chronicles grief, loss, and acceptance following Ollie’s death.</p>"))
write(f"{base_dir}/events/simon_story.html", page("Simon’s Story", event_links, "<h2>Simon’s Story</h2><p>Details Simon’s descent, loss of faith, and ultimate fate.</p>"))
write(f"{base_dir}/events/imp_story.html", page("Imp’s Story", event_links, "<h2>Imp’s Story</h2><p>Explores Imp’s crimes, guilt, and moral decay.</p>"))

# Zip it
zip_path = "/mnt/data/rebirth_wiki.zip"
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    for root, _, files in os.walk(base_dir):
        for f in files:
            full = os.path.join(root, f)
            z.write(full, arcname=os.path.relpath(full, base_dir))

zip_path
