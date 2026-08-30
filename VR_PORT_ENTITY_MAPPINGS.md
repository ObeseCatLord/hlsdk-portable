# They Hunger VR adapter entity mappings

This branch keeps Lambda1VR's optional `vr_client_api.h` presentation adapter
and routes gameplay from the server's fresh tracked weapon pose.  It is also
the source mapping for the Sven multiplayer conversion adapter; do not rename
these entity classes when reusing the implementation.

| Entity classname | Server class | VR interaction |
| --- | --- | --- |
| `weapon_crowbar` | `CCrowbar` | Physical tracked swing, stock button fallback, haptic impact |
| `weapon_th_shovel` | `CWeaponEinarShovel` | Tracked aim plus physical swing parity |
| `weapon_th_spanner` | `CWeaponEinarSpanner` | Tracked aim plus physical swing parity |
| `weapon_th_ap9` | `CWeaponEinarAP9` | Tracked hitscan origin/direction |
| `weapon_th_taurus` | `CWeaponEinarTaurus` | Tracked hitscan origin/direction |
| `weapon_th_sniper`, `weapon_einar1` | `CWeaponEinarSniper`, `CWeaponEinarTFCSniper` | Tracked hitscan and proximity scope |
| `weapon_th_chaingun`, `weapon_hornetgun` | `CWeaponEinarChaingun` | Tracked hitscan origin/direction |
| `weapon_egon` | `CEgon` | Einar flame projectile spawn and direction from tracked weapon pose |
| `einar_flame` | `CEinarFlameRocket` | Projectile retains expansion flame behavior; it consumes the firing pose above |
| `monster_th_*`, `einar_*` monsters | Hunger monster classes | No player-held VR path; preserve stock campaign AI and attacks |

Base entities used by the adapter retain their original names and classes:
`weapon_glock`/`CGlock`, `weapon_357`/`CPython`, `weapon_9mmAR`/`CMP5`,
`weapon_shotgun`/`CShotgun`, `weapon_crossbow`/`CCrossbow`,
`weapon_rpg`/`CRpg`, `weapon_gauss`/`CGauss`, `weapon_hornetgun` where not
overridden by Hunger, and the timed/deployed item classes (`CGrenade`,
`CSatchelCharge`, `CTripmineGrenade`, `CSqueakGrenade`).

`updatevr` accepts exactly 15 finite float arguments: weapon position, weapon
angles, weapon velocity, offhand position, and offhand angles. `vruse2`
accepts exactly `0` or `1`.  Pose freshness gates all server-side tracked
interaction, with conventional view/button paths retained as fallback.
