cmake_minimum_required(VERSION 2.8)

find_package(wxWidgets REQUIRED all)
include(${wxWidgets_USE_FILE})

set(WXCROOT ${PROJECT_SOURCE_DIR}/wxHaskell/wxc/src/)
set(WXCINCLUDE ${WXCROOT}include/)
set(WXCSRC     ${WXCROOT}cpp/)

include_directories(
    ${WXCINCLUDE}
)

add_definitions(
    -DwxcREFUSE_MEDIACTRL
)

add_custom_target(patch_wxc_glue_h
    patch -N -p1 < ${PROJECT_SOURCE_DIR}/wxc/wxc_glue_h.patch || /usr/bin/true
    DEPENDS        ${PROJECT_SOURCE_DIR}/wxc/wxc_glue_h.patch
    WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}/wxHaskell
)

add_library(wxc SHARED
    ${WXCSRC}apppath.cpp
    ${WXCSRC}dragimage.cpp
    ${WXCSRC}eljaccelerator.cpp
    ${WXCSRC}eljartprov.cpp
    ${WXCSRC}eljbitmap.cpp
    ${WXCSRC}eljbrush.cpp
    ${WXCSRC}eljbusyinfo.cpp
    ${WXCSRC}eljbutton.cpp
    ${WXCSRC}eljcalendarctrl.cpp
    ${WXCSRC}eljcaret.cpp
    ${WXCSRC}eljcheckbox.cpp
    ${WXCSRC}eljchecklistbox.cpp
    ${WXCSRC}eljchoice.cpp
    ${WXCSRC}eljclipboard.cpp
    ${WXCSRC}eljcoldata.cpp
    ${WXCSRC}eljcolour.cpp
    ${WXCSRC}eljcolourdlg.cpp
    ${WXCSRC}eljcombobox.cpp
    ${WXCSRC}eljconfigbase.cpp
    ${WXCSRC}eljcontrol.cpp
    ${WXCSRC}eljctxhelp.cpp
    ${WXCSRC}eljcursor.cpp
    ${WXCSRC}eljdataformat.cpp
    ${WXCSRC}eljdatetime.cpp
    ${WXCSRC}eljdc.cpp
    ${WXCSRC}eljdcsvg.cpp
    ${WXCSRC}eljdialog.cpp
    ${WXCSRC}eljdirdlg.cpp
    ${WXCSRC}eljdnd.cpp
    ${WXCSRC}eljdrawing.cpp
    ${WXCSRC}eljevent.cpp
    ${WXCSRC}eljfiledialog.cpp
    ${WXCSRC}eljfilehist.cpp
    ${WXCSRC}eljfindrepldlg.cpp
    ${WXCSRC}eljfont.cpp
    ${WXCSRC}eljfontdata.cpp
    ${WXCSRC}eljfontdlg.cpp
    ${WXCSRC}eljframe.cpp
    ${WXCSRC}eljgauge.cpp
    ${WXCSRC}eljgrid.cpp
    ${WXCSRC}eljhelpcontroller.cpp
    ${WXCSRC}eljicnbndl.cpp
    ${WXCSRC}eljicon.cpp
    ${WXCSRC}eljimage.cpp
    ${WXCSRC}eljimagelist.cpp
    ${WXCSRC}eljlayoutconstraints.cpp
    ${WXCSRC}eljlistbox.cpp
    ${WXCSRC}eljlistctrl.cpp
    ${WXCSRC}eljlocale.cpp
    ${WXCSRC}eljlog.cpp
    ${WXCSRC}eljmask.cpp
    ${WXCSRC}eljmdi.cpp
    ${WXCSRC}eljmenu.cpp
    ${WXCSRC}eljmenubar.cpp
    ${WXCSRC}eljmessagedialog.cpp
    ${WXCSRC}eljmime.cpp
    ${WXCSRC}eljminiframe.cpp
    ${WXCSRC}eljnotebook.cpp
    ${WXCSRC}eljpalette.cpp
    ${WXCSRC}eljpanel.cpp
    ${WXCSRC}eljpen.cpp
    ${WXCSRC}eljprintdlg.cpp
    ${WXCSRC}eljprinting.cpp
    ${WXCSRC}eljprocess.cpp
    ${WXCSRC}eljradiobox.cpp
    ${WXCSRC}eljradiobutton.cpp
    ${WXCSRC}eljrc.cpp
    ${WXCSRC}eljregion.cpp
    ${WXCSRC}eljregioniter.cpp
    ${WXCSRC}eljsash.cpp
    ${WXCSRC}eljscrollbar.cpp
    ${WXCSRC}eljscrolledwindow.cpp
    ${WXCSRC}eljsingleinst.cpp
    ${WXCSRC}eljsizer.cpp
    ${WXCSRC}eljslider.cpp
    ${WXCSRC}eljspinctrl.cpp
    ${WXCSRC}eljsplitterwindow.cpp
    ${WXCSRC}eljstaticbox.cpp
    ${WXCSRC}eljstaticline.cpp
    ${WXCSRC}eljstatictext.cpp
    ${WXCSRC}eljstatusbar.cpp
    ${WXCSRC}eljsystemsettings.cpp
    ${WXCSRC}eljtextctrl.cpp
    ${WXCSRC}eljtimer.cpp
    ${WXCSRC}eljtipwnd.cpp
    ${WXCSRC}eljtglbtn.cpp
    ${WXCSRC}eljtoolbar.cpp
    ${WXCSRC}eljvalidator.cpp
    ${WXCSRC}eljwindow.cpp
    ${WXCSRC}eljwizard.cpp
    ${WXCSRC}ewxw_main.cpp
    ${WXCSRC}extra.cpp
    ${WXCSRC}glcanvas.cpp
    ${WXCSRC}graphicscontext.cpp
    ${WXCSRC}image.cpp
    ${WXCSRC}managed.cpp
    ${WXCSRC}mediactrl.cpp
    ${WXCSRC}previewframe.cpp
    ${WXCSRC}printout.cpp
    ${WXCSRC}sckaddr.cpp
    ${WXCSRC}socket.cpp
    ${WXCSRC}sound.cpp
    ${WXCSRC}stc.cpp
    ${WXCSRC}std.cpp
    ${WXCSRC}taskbaricon.cpp
    ${WXCSRC}textstream.cpp
    ${WXCSRC}treectrl.cpp
    ${WXCSRC}wrapper.cpp
)

add_dependencies(wxc
    patch_wxc_glue_h
)

target_link_libraries(wxc
    ${wxWidgets_LIBRARIES}
)
