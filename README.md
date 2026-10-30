# EAS-4-TbSync

> [!IMPORTANT]
> **This is an unofficial fork with unofficial builds.**
>
> It is not the official EAS-4-TbSync, and it is not released, reviewed or endorsed
> by the upstream maintainer. The official project is
> [jobisoft/EAS-4-TbSync](https://github.com/jobisoft/EAS-4-TbSync).
>
> The `compat` branch of this fork only carries compatibility fixes from
> upstream pull requests, so EAS-4-TbSync keeps working on Thunderbird releases the
> official version does not support yet. What a build contains and how to
> verify a download is described in [COMPAT.md](COMPAT.md).
>
> - **No warranty.** The builds are provided "as is", without warranty of any
>   kind. Liability is excluded to the extent permitted by applicable law, as
>   set out in sections 6 and 7 of the [Mozilla Public License 2.0](LICENSE).
> - **No support.** We do not offer support for these builds.
> - **Do not report problems with these builds upstream.**
> - As soon as an official release supports your Thunderbird version, use that
>   instead.

This provider add-on adds Exchange ActiveSync (EAS v2.5, v14.0, 14.1 & v16.1) synchronization capabilities to [TbSync](https://github.com/jobisoft/TbSync/).

More information can be found in the [wiki](https://github.com/jobisoft/EAS-4-TbSync/wiki/About:-Provider-for-Exchange-ActiveSync) of this repository

## Known limitations

### Recurring events from a foreign time zone (±1 hour DST drift)

A recurring series can drift by one hour around daylight-saving transitions,
but only when all three of these hold at once:

1. the series was authored in a time zone other than your Thunderbird default
   zone, **and**
2. the server sends no usable `TimeZone` blob — Z-Push, Kopano and Grommunio
   send an all-zero one, **and**
3. the occurrence falls in a different DST state than the series master.

The authoring zone is then simply not transmitted, so the series anchors to
your default zone. This is inherent to what the protocol carries; the client
cannot recover it.

**Not affected:** Exchange on any version, including 16.0/16.1 — it sends a
full `TimeZone` blob, which is matched back to the correct IANA zone
(same-offset zones such as Berlin and Paris are told apart by their DST
transition dates). Single events are never affected, since their exact UTC
instant is always preserved. Neither are incoming all-day events. Pushing an
all-day event *back* to a non-Exchange server that ignores the blob we send
can still shift the date by a day for users east of UTC.

## Want to add or fix a localization?
To help translating this project, please visit [crowdin.com](https://crowdin.com/profile/jobisoft), where the localizations are managed. If you want to add a new language, just contact me and I will set it up.


## External data sources

* TbSync uses a [timezone mapping](https://github.com/mattjohnsonpint/TimeZoneConverter/blob/master/src/TimeZoneConverter/Data/Mapping.csv.gz) provided by [Matt Johnson-Pint](https://github.com/mattjohnsonpint)


## Icon sources and attributions

#### CC0 Public Domain
* [365_*.png] by [Microsoft / Wikimedia](https://commons.wikimedia.org/w/index.php?curid=21546299), converted from [SVG to PNG](https://ezgif.com/svg-to-png)

#### CC-BY 3.0
* [eas*.png] by [FatCow Web Hosting](https://www.iconfinder.com/icons/64484/exchange_ms_icon)
* [exchange_300.png] derived from [Microsoft Exchange Icon #270871](https://icon-library.net/icon/microsoft-exchange-icon-10.html), [resized](www.simpleimageresizer.com/)
