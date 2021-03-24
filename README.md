```
CREATE TABLE `tibia_auction` (
`id` int(11) NOT NULL,
`character_name` varchar(255) DEFAULT NULL,
`level` int(11) NOT NULL DEFAULT '0',
`vocation` varchar(25) DEFAULT NULL,
`gender` varchar(6) DEFAULT NULL,
`world_name` varchar(25) DEFAULT NULL,
`world_type` varchar(25) DEFAULT NULL,
`world_blocked` tinyint(1) NOT NULL DEFAULT '0',
`world_premium` tinyint(1) NOT NULL DEFAULT '0',
`world_battleye` varchar(10) DEFAULT NULL,
`bid_amount` int(11) NOT NULL DEFAULT '0',
`bid_type` varchar(25) DEFAULT NULL,

`skill_axe` int(11) NOT NULL DEFAULT '0',
`skill_club` int(11) NOT NULL DEFAULT '0',
`skill_distance` int(11) NOT NULL DEFAULT '0',
`skill_fishing` int(11) NOT NULL DEFAULT '0',
`skill_fist` int(11) NOT NULL DEFAULT '0',
`skill_magic` int(11) NOT NULL DEFAULT '0',
`skill_shielding` int(11) NOT NULL DEFAULT '0',
`skill_sword` int(11) NOT NULL DEFAULT '0',


`charms` int(11) NOT NULL DEFAULT '0',
`achievements` int(11) NOT NULL DEFAULT '0',
`prey_slots` int(11) NOT NULL DEFAULT '0',
`hunt_slots` int(11) NOT NULL DEFAULT '0',
`imbuements` int(11) NOT NULL DEFAULT '0',
`imbuements_info` varchar(2000) DEFAULT NULL,
`auction_start` int(11) NOT NULL DEFAULT '0',
`auction_end` int(11) NOT NULL DEFAULT '0',

`items` longtext,
`page_html_gzcompressed` MEDIUMBLOB,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;


public function getPageHtmlGzcompressed()
{
    if($this->pageHtmlGzcompressed !== null)
    {
        if(is_string($this->pageHtmlGzcompressed))
        {
            return gzuncompress($this->pageHtmlGzcompressed);
        }
        $result = @gzuncompress(stream_get_contents($this->pageHtmlGzcompressed));
        if ($result === false) {
            $result = @gzuncompress( stream_get_contents($this->pageHtmlGzcompressed, 1, 0 ) . stream_get_contents( $this->pageHtmlGzcompressed, -1, 1 ) );
            if ($result === false) {
                var_dump($this->id);
                exit;
            }
        }
        return $result;
    }
    else
    {
        return $this->pageHtmlGzcompressed;
    }
}

```