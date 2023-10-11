#!/bin/sh

set -e

# if no arguments are passed, return the extension's manifest
if [ $# -eq 0 ]; then
  sunbeam query -n '{
    title: "DevDocs",
    commands: [
      {
        name: "list-docsets",
        title: "List Docsets",
        mode: "view"
      },
      {
        name: "list-entries",
        title: "List Entries from Docset",
        mode: "view",
        params: [
          {name: "slug", type: "string", required: true, description: "docset to search"}
        ]
      }
    ]
  }'
  exit 0
fi

if [ "$1" = "list-docsets" ]; then
  # shellcheck disable=SC2016
  sunbeam fetch https://devdocs.io/docs/docs.json | sunbeam query 'map({
      title: .name,
      subtitle: (.release // "latest"),
      accessories: [ .slug ],
      actions: [
        {
          title: "Browse entries",
          onAction: {
            type: "run",
            command: "list-entries",
            params: {
              slug: .slug
            }
          }
        }
      ]
    }) | { type: "list", items: . }'
elif [ "$1" = "list-entries" ]; then
  SLUG=$(sunbeam query -r '.params.slug')
  # shellcheck disable=SC2016
  sunbeam fetch "https://devdocs.io/docs/$SLUG/index.json" | sunbeam query --arg slug="$SLUG" '.entries | map({
      title: .name,
      subtitle: .type,
      actions: [
        {title: "Open in Browser", onAction: { type: "open", target: "https://devdocs.io/\($slug)/\(.path)", exit: true}},
        {title: "Copy URL", key: "c", onAction: { type: "copy", text: "https://devdocs.io/\($slug)/\(.path)", exit: true}}
      ]
    }) | { type: "list", items: . }'
fi
