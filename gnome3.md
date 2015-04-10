# gnome3

## hide the title bar

Gnome 3.16 changes to the window decoration code (dropping support for the old Metacity format).

        # vim /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml
        
        <frame_geometry name="max" has_title="false" title_scale="medium" parent="normal" rounded_top_left="false" rounded_top_right="false">
            <distance name="left_width" value="0" />
            <distance name="right_width" value="0" />
            <distance name="title_vertical_pad" value="0"/> <!-- 
                                    This needs to be 1 less then the
                                    title_vertical_pad on normal state
                                    or you'll have bigger buttons                               -->
            <border name="title_border" left="10" right="10" top="0" bottom="0"/>
            <border name="button_border" left="0" right="0" top="0" bottom="0"/>
            <distance name="bottom_height" value="0" />
        </frame_geometry>
