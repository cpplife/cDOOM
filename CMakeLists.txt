cmake_minimum_required (VERSION 3.10.1)


project(cDOOM)

###############################################################################
# Set project output dirs
###############################################################################
set(PROJECT_OUT_LIB ${CMAKE_BINARY_DIR}/lib)
set(PROJECT_OUT_BIN ${CMAKE_BINARY_DIR}/bin)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_OUT_LIB})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_OUT_LIB})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_OUT_BIN})


#Add specific macros
set(PROJECT_FLAGS "-D__DOOM__ -D_CRT_SECURE_NO_DEPRECATE -D_CRT_NONSTDC_NO_DEPRECATE -D_USE_32BIT_TIME_T -D_MBCS")
set(CMAKE_C_FLAGS " ${PROJECT_FLAGS}")
set(CMAKE_CXX_FLAGS " ${PROJECT_FLAGS}")

# Set Project dir
set(PROJECT_DIR ${CMAKE_CURRENT_LIST_DIR})

# Set directx dirs
set(DX_LIB_DIR ${PROJECT_DIR}/dxsdk_june2010/lib)
if(CMAKE_SIZEOF_VOID_P EQUAL 8)
    # 64 bits
	set(DX_LIB_DIR ${DX_LIB_DIR}/x64)
elseif(CMAKE_SIZEOF_VOID_P EQUAL 4)
	set(DX_LIB_DIR ${DX_LIB_DIR}/x86)
endif()


###############################################################################
# depend projects
###############################################################################
# Build doomclassic
add_subdirectory( doomclassic )

###############################################################################
# project code
###############################################################################
set(SRCS_CODE
	${PROJECT_DIR}/neo/aas/AASFile.cpp
    ${PROJECT_DIR}/neo/aas/AASFileManager.cpp
    ${PROJECT_DIR}/neo/aas/AASFile_optimize.cpp
    ${PROJECT_DIR}/neo/aas/AASFile_sample.cpp
    ${PROJECT_DIR}/neo/cm/CollisionModel_contacts.cpp
    ${PROJECT_DIR}/neo/cm/CollisionModel_contents.cpp
    ${PROJECT_DIR}/neo/cm/CollisionModel_debug.cpp
    ${PROJECT_DIR}/neo/cm/CollisionModel_files.cpp
    ${PROJECT_DIR}/neo/cm/CollisionModel_load.cpp
    ${PROJECT_DIR}/neo/cm/CollisionModel_rotate.cpp
    ${PROJECT_DIR}/neo/cm/CollisionModel_trace.cpp
    ${PROJECT_DIR}/neo/cm/CollisionModel_translate.cpp
    ${PROJECT_DIR}/neo/d3xp/Achievements.cpp
    ${PROJECT_DIR}/neo/d3xp/Actor.cpp
    ${PROJECT_DIR}/neo/d3xp/AF.cpp
    ${PROJECT_DIR}/neo/d3xp/AFEntity.cpp
    ${PROJECT_DIR}/neo/d3xp/AimAssist.cpp
    ${PROJECT_DIR}/neo/d3xp/ai/AAS.cpp
    ${PROJECT_DIR}/neo/d3xp/ai/AAS_debug.cpp
    ${PROJECT_DIR}/neo/d3xp/ai/AAS_pathing.cpp
    ${PROJECT_DIR}/neo/d3xp/ai/AAS_routing.cpp
    ${PROJECT_DIR}/neo/d3xp/ai/AI.cpp
    ${PROJECT_DIR}/neo/d3xp/ai/AI_events.cpp
    ${PROJECT_DIR}/neo/d3xp/ai/AI_pathing.cpp
    ${PROJECT_DIR}/neo/d3xp/ai/AI_Vagary.cpp
    ${PROJECT_DIR}/neo/d3xp/anim/Anim.cpp
    ${PROJECT_DIR}/neo/d3xp/anim/Anim_Blend.cpp
    ${PROJECT_DIR}/neo/d3xp/anim/Anim_Testmodel.cpp
    ${PROJECT_DIR}/neo/d3xp/BrittleFracture.cpp
    ${PROJECT_DIR}/neo/d3xp/Camera.cpp
    ${PROJECT_DIR}/neo/d3xp/Entity.cpp
    ${PROJECT_DIR}/neo/d3xp/Fx.cpp
    ${PROJECT_DIR}/neo/d3xp/GameEdit.cpp
    ${PROJECT_DIR}/neo/d3xp/gamesys/Class.cpp
    ${PROJECT_DIR}/neo/d3xp/gamesys/Event.cpp
    ${PROJECT_DIR}/neo/d3xp/gamesys/SaveGame.cpp
    ${PROJECT_DIR}/neo/d3xp/gamesys/SysCmds.cpp
    ${PROJECT_DIR}/neo/d3xp/gamesys/SysCvar.cpp
    ${PROJECT_DIR}/neo/d3xp/Game_local.cpp
    ${PROJECT_DIR}/neo/d3xp/Game_network.cpp
    ${PROJECT_DIR}/neo/d3xp/Grabber.cpp
    ${PROJECT_DIR}/neo/d3xp/IK.cpp
    ${PROJECT_DIR}/neo/d3xp/Item.cpp
    ${PROJECT_DIR}/neo/d3xp/Leaderboards.cpp
    ${PROJECT_DIR}/neo/d3xp/Light.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuHandler.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuHandler_HUD.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuHandler_PDA.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuHandler_Scoreboard.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuHandler_Shell.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_HUD.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_PDA_Inventory.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_PDA_UserData.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_PDA_UserEmails.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_PDA_VideoDisks.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Scoreboard.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Bindings.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Browser.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_ControllerLayout.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Controls.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Credits.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Dev.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Difficulty.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_GameLobby.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_GameOptions.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Gamepad.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Leaderboards.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Load.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_MatchSettings.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_ModeSelect.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_NewGame.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_PartyLobby.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Pause.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Playstation.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_PressStart.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Resolution.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Root.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Save.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Settings.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Singleplayer.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_Stereoscopics.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuScreen_Shell_SystemOptions.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_Button.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_Carousel.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_CommandBar.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_DynamicList.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_Help.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_InfoBox.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_ItemAssignment.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_List.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_LobbyList.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_MenuBar.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_NavBar.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_NavButton.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_PDA_AudioFiles.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_PDA_EmailInbox.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_PDA_Objective.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_PDA_UserData.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_PDA_VideoInfo.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_Scrollbar.cpp
    ${PROJECT_DIR}/neo/d3xp/menus/MenuWidget_Shell_SaveInfo.cpp
    ${PROJECT_DIR}/neo/d3xp/Misc.cpp
    ${PROJECT_DIR}/neo/d3xp/Moveable.cpp
    ${PROJECT_DIR}/neo/d3xp/Mover.cpp
    ${PROJECT_DIR}/neo/d3xp/MultiplayerGame.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Clip.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Force.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Force_Constant.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Force_Drag.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Force_Field.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Force_Grab.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Force_Spring.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Physics.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Physics_Actor.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Physics_AF.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Physics_Base.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Physics_Monster.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Physics_Parametric.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Physics_Player.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Physics_RigidBody.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Physics_Static.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Physics_StaticMulti.cpp
    ${PROJECT_DIR}/neo/d3xp/physics/Push.cpp
    ${PROJECT_DIR}/neo/d3xp/Player.cpp
    ${PROJECT_DIR}/neo/d3xp/PlayerIcon.cpp
    ${PROJECT_DIR}/neo/d3xp/PlayerView.cpp
    ${PROJECT_DIR}/neo/d3xp/d3xp_precompiled.cpp
    ${PROJECT_DIR}/neo/d3xp/Projectile.cpp
    ${PROJECT_DIR}/neo/d3xp/Pvs.cpp
    ${PROJECT_DIR}/neo/d3xp/script/Script_Compiler.cpp
    ${PROJECT_DIR}/neo/d3xp/script/Script_Interpreter.cpp
    ${PROJECT_DIR}/neo/d3xp/script/Script_Program.cpp
    ${PROJECT_DIR}/neo/d3xp/script/Script_Thread.cpp
    ${PROJECT_DIR}/neo/d3xp/SecurityCamera.cpp
    ${PROJECT_DIR}/neo/d3xp/SmokeParticles.cpp
    ${PROJECT_DIR}/neo/d3xp/Sound.cpp
    ${PROJECT_DIR}/neo/d3xp/Target.cpp
    ${PROJECT_DIR}/neo/d3xp/Trigger.cpp
    ${PROJECT_DIR}/neo/d3xp/Weapon.cpp
    ${PROJECT_DIR}/neo/d3xp/WorldSpawn.cpp
    ${PROJECT_DIR}/neo/framework/CmdSystem.cpp
    ${PROJECT_DIR}/neo/framework/Common.cpp
    ${PROJECT_DIR}/neo/framework/Common_demos.cpp
    ${PROJECT_DIR}/neo/framework/Common_dialog.cpp
    ${PROJECT_DIR}/neo/framework/common_frame.cpp
    ${PROJECT_DIR}/neo/framework/Common_localize.cpp
    ${PROJECT_DIR}/neo/framework/Common_menu.cpp
    ${PROJECT_DIR}/neo/framework/Common_network.cpp
    ${PROJECT_DIR}/neo/framework/Common_printf.cpp
    ${PROJECT_DIR}/neo/framework/Common_load.cpp
    ${PROJECT_DIR}/neo/framework/Compressor.cpp
    ${PROJECT_DIR}/neo/framework/Console.cpp
    ${PROJECT_DIR}/neo/framework/ConsoleHistory.cpp
    ${PROJECT_DIR}/neo/framework/CVarSystem.cpp
    ${PROJECT_DIR}/neo/framework/DebugGraph.cpp
    ${PROJECT_DIR}/neo/framework/DeclAF.cpp
    ${PROJECT_DIR}/neo/framework/DeclEntityDef.cpp
    ${PROJECT_DIR}/neo/framework/DeclFX.cpp
    ${PROJECT_DIR}/neo/framework/DeclManager.cpp
    ${PROJECT_DIR}/neo/framework/DeclParticle.cpp
    ${PROJECT_DIR}/neo/framework/DeclPDA.cpp
    ${PROJECT_DIR}/neo/framework/DeclSkin.cpp
    ${PROJECT_DIR}/neo/framework/DeclTable.cpp
    ${PROJECT_DIR}/neo/framework/DemoFile.cpp
    ${PROJECT_DIR}/neo/framework/EditField.cpp
    ${PROJECT_DIR}/neo/framework/EventLoop.cpp
    ${PROJECT_DIR}/neo/framework/File.cpp
    ${PROJECT_DIR}/neo/framework/FileSystem.cpp
    ${PROJECT_DIR}/neo/framework/File_Manifest.cpp
    ${PROJECT_DIR}/neo/framework/File_Resource.cpp
    ${PROJECT_DIR}/neo/framework/File_SaveGame.cpp
    ${PROJECT_DIR}/neo/framework/KeyInput.cpp
    ${PROJECT_DIR}/neo/framework/PlayerProfile.cpp
    ${PROJECT_DIR}/neo/framework/framework_precompiled.cpp
    ${PROJECT_DIR}/neo/framework/TokenParser.cpp
    ${PROJECT_DIR}/neo/framework/Unzip.cpp
    ${PROJECT_DIR}/neo/framework/UsercmdGen.cpp
    ${PROJECT_DIR}/neo/framework/Zip.cpp
    ${PROJECT_DIR}/neo/framework/zlib/adler32.c
    ${PROJECT_DIR}/neo/framework/zlib/compress.c
    ${PROJECT_DIR}/neo/framework/zlib/crc32.c
    ${PROJECT_DIR}/neo/framework/zlib/deflate.c
    ${PROJECT_DIR}/neo/framework/zlib/example.c
    ${PROJECT_DIR}/neo/framework/zlib/gzio.c
    ${PROJECT_DIR}/neo/framework/zlib/infback.c
    ${PROJECT_DIR}/neo/framework/zlib/inffast.c
    ${PROJECT_DIR}/neo/framework/zlib/inflate.c
    ${PROJECT_DIR}/neo/framework/zlib/inftrees.c
    ${PROJECT_DIR}/neo/framework/zlib/trees.c
    ${PROJECT_DIR}/neo/framework/zlib/uncompr.c
    ${PROJECT_DIR}/neo/framework/zlib/zutil.c
    ${PROJECT_DIR}/neo/idlib/Base64.cpp
    ${PROJECT_DIR}/neo/idlib/BitMsg.cpp
    ${PROJECT_DIR}/neo/idlib/bv/Bounds.cpp
    ${PROJECT_DIR}/neo/idlib/bv/Box.cpp
    ${PROJECT_DIR}/neo/idlib/bv/Sphere.cpp
    ${PROJECT_DIR}/neo/idlib/CmdArgs.cpp
    ${PROJECT_DIR}/neo/idlib/CommandLink.cpp
    ${PROJECT_DIR}/neo/idlib/containers/HashIndex.cpp
    ${PROJECT_DIR}/neo/idlib/Dict.cpp
    ${PROJECT_DIR}/neo/idlib/geometry/DrawVert.cpp
    ${PROJECT_DIR}/neo/idlib/geometry/JointTransform.cpp
    ${PROJECT_DIR}/neo/idlib/geometry/RenderMatrix.cpp
    ${PROJECT_DIR}/neo/idlib/geometry/Surface.cpp
    ${PROJECT_DIR}/neo/idlib/geometry/Surface_Patch.cpp
    ${PROJECT_DIR}/neo/idlib/geometry/Surface_Polytope.cpp
    ${PROJECT_DIR}/neo/idlib/geometry/Surface_SweptSpline.cpp
    ${PROJECT_DIR}/neo/idlib/geometry/TraceModel.cpp
    ${PROJECT_DIR}/neo/idlib/geometry/Winding.cpp
    ${PROJECT_DIR}/neo/idlib/geometry/Winding2D.cpp
    ${PROJECT_DIR}/neo/idlib/hashing/idlib_CRC32.cpp
    ${PROJECT_DIR}/neo/idlib/hashing/MD4.cpp
    ${PROJECT_DIR}/neo/idlib/hashing/MD5.cpp
    ${PROJECT_DIR}/neo/idlib/Heap.cpp
    ${PROJECT_DIR}/neo/idlib/LangDict.cpp
    ${PROJECT_DIR}/neo/idlib/Lexer.cpp
    ${PROJECT_DIR}/neo/idlib/Lib.cpp
    ${PROJECT_DIR}/neo/idlib/MapFile.cpp
    ${PROJECT_DIR}/neo/idlib/math/Angles.cpp
    ${PROJECT_DIR}/neo/idlib/math/Complex.cpp
    ${PROJECT_DIR}/neo/idlib/math/Lcp.cpp
    ${PROJECT_DIR}/neo/idlib/math/Math.cpp
    ${PROJECT_DIR}/neo/idlib/math/Matrix.cpp
    ${PROJECT_DIR}/neo/idlib/math/MatX.cpp
    ${PROJECT_DIR}/neo/idlib/math/Ode.cpp
    ${PROJECT_DIR}/neo/idlib/math/Plane.cpp
    ${PROJECT_DIR}/neo/idlib/math/Pluecker.cpp
    ${PROJECT_DIR}/neo/idlib/math/Polynomial.cpp
    ${PROJECT_DIR}/neo/idlib/math/Quat.cpp
    ${PROJECT_DIR}/neo/idlib/math/Rotation.cpp
    ${PROJECT_DIR}/neo/idlib/math/Simd.cpp
    ${PROJECT_DIR}/neo/idlib/math/Simd_Generic.cpp
    ${PROJECT_DIR}/neo/idlib/math/Simd_SSE.cpp
    ${PROJECT_DIR}/neo/idlib/math/Vector.cpp
    ${PROJECT_DIR}/neo/idlib/math/VecX.cpp
    ${PROJECT_DIR}/neo/idlib/ParallelJobList.cpp
    ${PROJECT_DIR}/neo/idlib/Parser.cpp
    ${PROJECT_DIR}/neo/idlib/idlib_precompiled.cpp
    ${PROJECT_DIR}/neo/idlib/RectAllocator.cpp
    ${PROJECT_DIR}/neo/idlib/SoftwareCache.cpp
    ${PROJECT_DIR}/neo/idlib/Str.cpp
    ${PROJECT_DIR}/neo/idlib/sys/sys_assert.cpp
    ${PROJECT_DIR}/neo/idlib/sys/win32/win_thread.cpp
    ${PROJECT_DIR}/neo/idlib/Thread.cpp
    ${PROJECT_DIR}/neo/idlib/Timer.cpp
    ${PROJECT_DIR}/neo/idlib/Token.cpp
    ${PROJECT_DIR}/neo/renderer/AutoRender.cpp
    ${PROJECT_DIR}/neo/renderer/AutoRenderBink.cpp
    ${PROJECT_DIR}/neo/renderer/BinaryImage.cpp
    ${PROJECT_DIR}/neo/renderer/BufferObject.cpp
    ${PROJECT_DIR}/neo/renderer/Cinematic.cpp
    ${PROJECT_DIR}/neo/renderer/Color/ColorSpace.cpp
    ${PROJECT_DIR}/neo/renderer/DXT/DXTDecoder.cpp
    ${PROJECT_DIR}/neo/renderer/DXT/DXTEncoder.cpp
    ${PROJECT_DIR}/neo/renderer/DXT/DXTEncoder_SSE2.cpp
    ${PROJECT_DIR}/neo/renderer/Font.cpp
    ${PROJECT_DIR}/neo/renderer/GLMatrix.cpp
    ${PROJECT_DIR}/neo/renderer/GuiModel.cpp
    ${PROJECT_DIR}/neo/renderer/Image_files.cpp
    ${PROJECT_DIR}/neo/renderer/ImageManager.cpp
    ${PROJECT_DIR}/neo/renderer/Image_intrinsic.cpp
    ${PROJECT_DIR}/neo/renderer/Image_load.cpp
    ${PROJECT_DIR}/neo/renderer/Image_process.cpp
    ${PROJECT_DIR}/neo/renderer/Image_program.cpp
    ${PROJECT_DIR}/neo/renderer/Interaction.cpp
    ${PROJECT_DIR}/neo/renderer/jobs/prelightshadowvolume/PreLightShadowVolume.cpp
    ${PROJECT_DIR}/neo/renderer/jobs/ShadowShared.cpp
    ${PROJECT_DIR}/neo/renderer/jobs/staticshadowvolume/StaticShadowVolume.cpp
    ${PROJECT_DIR}/neo/renderer/jobs/dynamicshadowvolume/DynamicShadowVolume.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jcapimin.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jccoefct.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jccolor.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jcdctmgr.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jchuff.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jcinit.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jcmainct.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jcmarker.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jcmaster.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jcomapi.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jcparam.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jcphuff.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jcprepct.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jcsample.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdapimin.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdapistd.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdatadst.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdatasrc.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdcoefct.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdcolor.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jddctmgr.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdhuff.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdinput.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdmainct.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdmarker.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdmaster.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdmerge.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdphuff.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdpostct.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdsample.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jdtrans.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jerror.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jfdctflt.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jfdctfst.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jfdctint.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jidctflt.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jidctfst.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jidctint.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jidctred.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jmemmgr.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jmemnobs.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jquant1.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jquant2.cpp
    ${PROJECT_DIR}/neo/renderer/jpeg-6/jutils.cpp
    ${PROJECT_DIR}/neo/renderer/Material.cpp
    ${PROJECT_DIR}/neo/renderer/Model.cpp
    ${PROJECT_DIR}/neo/renderer/Model_ase.cpp
    ${PROJECT_DIR}/neo/renderer/Model_beam.cpp
    ${PROJECT_DIR}/neo/renderer/Model_liquid.cpp
    ${PROJECT_DIR}/neo/renderer/Model_lwo.cpp
    ${PROJECT_DIR}/neo/renderer/Model_ma.cpp
    ${PROJECT_DIR}/neo/renderer/Model_md3.cpp
    ${PROJECT_DIR}/neo/renderer/Model_md5.cpp
    ${PROJECT_DIR}/neo/renderer/Model_prt.cpp
    ${PROJECT_DIR}/neo/renderer/Model_sprite.cpp
    ${PROJECT_DIR}/neo/renderer/ModelDecal.cpp
    ${PROJECT_DIR}/neo/renderer/ModelManager.cpp
    ${PROJECT_DIR}/neo/renderer/ModelOverlay.cpp
    ${PROJECT_DIR}/neo/renderer/OpenGL/gl_GraphicsAPIWrapper.cpp
    ${PROJECT_DIR}/neo/renderer/OpenGL/gl_image.cpp
    ${PROJECT_DIR}/neo/renderer/OpenGL/gl_backend.cpp
    ${PROJECT_DIR}/neo/renderer/RenderProgs.cpp
    ${PROJECT_DIR}/neo/renderer/RenderProgs_GLSL.cpp
    ${PROJECT_DIR}/neo/renderer/RenderWorld_defs.cpp
    ${PROJECT_DIR}/neo/renderer/ResolutionScale.cpp
    ${PROJECT_DIR}/neo/renderer/RenderEntity.cpp
    ${PROJECT_DIR}/neo/renderer/RenderLog.cpp
    ${PROJECT_DIR}/neo/renderer/RenderSystem.cpp
    ${PROJECT_DIR}/neo/renderer/RenderSystem_init.cpp
    ${PROJECT_DIR}/neo/renderer/RenderWorld.cpp
    ${PROJECT_DIR}/neo/renderer/RenderWorld_demo.cpp
    ${PROJECT_DIR}/neo/renderer/RenderWorld_load.cpp
    ${PROJECT_DIR}/neo/renderer/RenderWorld_portals.cpp
    ${PROJECT_DIR}/neo/renderer/ScreenRect.cpp
    ${PROJECT_DIR}/neo/renderer/tr_backend_draw.cpp
    ${PROJECT_DIR}/neo/renderer/tr_backend_rendertools.cpp
    ${PROJECT_DIR}/neo/renderer/tr_frontend_addlights.cpp
    ${PROJECT_DIR}/neo/renderer/tr_frontend_addmodels.cpp
    ${PROJECT_DIR}/neo/renderer/tr_frontend_deform.cpp
    ${PROJECT_DIR}/neo/renderer/tr_frontend_guisurf.cpp
    ${PROJECT_DIR}/neo/renderer/tr_frontend_main.cpp
    ${PROJECT_DIR}/neo/renderer/tr_frontend_subview.cpp
    ${PROJECT_DIR}/neo/renderer/tr_trace.cpp
    ${PROJECT_DIR}/neo/renderer/tr_trisurf.cpp
    ${PROJECT_DIR}/neo/renderer/VertexCache.cpp
    ${PROJECT_DIR}/neo/sound/snd_emitter.cpp
    ${PROJECT_DIR}/neo/sound/snd_shader.cpp
    ${PROJECT_DIR}/neo/sound/snd_system.cpp
    ${PROJECT_DIR}/neo/sound/snd_world.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Bitstream.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Dictionary.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Events.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Image.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Load.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Main.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Names.cpp
    ${PROJECT_DIR}/neo/swf/SWF_ParmList.cpp
    ${PROJECT_DIR}/neo/swf/SWF_PlaceObject.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Render.cpp
    ${PROJECT_DIR}/neo/swf/SWF_ScriptFunction.cpp
    ${PROJECT_DIR}/neo/swf/SWF_ScriptObject.cpp
    ${PROJECT_DIR}/neo/swf/SWF_ScriptVar.cpp
    ${PROJECT_DIR}/neo/swf/SWF_ShapeParser.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Shapes.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Sounds.cpp
    ${PROJECT_DIR}/neo/swf/SWF_SpriteInstance.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Sprites.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Text.cpp
    ${PROJECT_DIR}/neo/swf/SWF_TextInstance.cpp
    ${PROJECT_DIR}/neo/swf/SWF_Zlib.cpp
    ${PROJECT_DIR}/neo/sys/LightweightCompression.cpp
    ${PROJECT_DIR}/neo/sys/PacketProcessor.cpp
    ${PROJECT_DIR}/neo/sys/Snapshot.cpp
    ${PROJECT_DIR}/neo/sys/SnapshotProcessor.cpp
    ${PROJECT_DIR}/neo/sys/Snapshot_Jobs.cpp
    ${PROJECT_DIR}/neo/sys/sys_achievements.cpp
    ${PROJECT_DIR}/neo/sys/sys_dedicated_server_search.cpp
    ${PROJECT_DIR}/neo/sys/sys_lobby.cpp
    ${PROJECT_DIR}/neo/sys/sys_lobby_backend_direct.cpp
    ${PROJECT_DIR}/neo/sys/sys_lobby_migrate.cpp
    ${PROJECT_DIR}/neo/sys/sys_lobby_snapshot.cpp
    ${PROJECT_DIR}/neo/sys/sys_lobby_users.cpp
    ${PROJECT_DIR}/neo/sys/sys_local.cpp
    ${PROJECT_DIR}/neo/sys/sys_localuser.cpp
    ${PROJECT_DIR}/neo/sys/sys_profile.cpp
    ${PROJECT_DIR}/neo/sys/sys_savegame.cpp
    ${PROJECT_DIR}/neo/sys/sys_session_callbacks.cpp
    ${PROJECT_DIR}/neo/sys/sys_session_local.cpp
    ${PROJECT_DIR}/neo/sys/sys_session_savegames.cpp
    ${PROJECT_DIR}/neo/sys/sys_signin.cpp
    ${PROJECT_DIR}/neo/sound/SoundVoice.cpp
    ${PROJECT_DIR}/neo/sound/WaveFile.cpp
    ${PROJECT_DIR}/neo/sound/XAudio2/XA2_SoundHardware.cpp
    ${PROJECT_DIR}/neo/sound/XAudio2/XA2_SoundSample.cpp
    ${PROJECT_DIR}/neo/sound/XAudio2/XA2_SoundVoice.cpp
    ${PROJECT_DIR}/neo/sys/sys_voicechat.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_achievements.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_cpu.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_glimp.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_input.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_localuser.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_main.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_net.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_qgl.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_savegame.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_session_local.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_shared.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_signin.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_snd.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_syscon.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_taskkeyhook.cpp
    ${PROJECT_DIR}/neo/sys/win32/win_wndproc.cpp
    ${PROJECT_DIR}/neo/ui/BindWindow.cpp
    ${PROJECT_DIR}/neo/ui/ChoiceWindow.cpp
    ${PROJECT_DIR}/neo/ui/DeviceContext.cpp
    ${PROJECT_DIR}/neo/ui/EditWindow.cpp
    ${PROJECT_DIR}/neo/ui/FieldWindow.cpp
    ${PROJECT_DIR}/neo/ui/GameBearShootWindow.cpp
    ${PROJECT_DIR}/neo/ui/GameBustOutWindow.cpp
    ${PROJECT_DIR}/neo/ui/GameSSDWindow.cpp
    ${PROJECT_DIR}/neo/ui/GuiScript.cpp
    ${PROJECT_DIR}/neo/ui/ListGUI.cpp
    ${PROJECT_DIR}/neo/ui/ListWindow.cpp
    ${PROJECT_DIR}/neo/ui/RegExp.cpp
    ${PROJECT_DIR}/neo/ui/RenderWindow.cpp
    ${PROJECT_DIR}/neo/ui/SimpleWindow.cpp
    ${PROJECT_DIR}/neo/ui/SliderWindow.cpp
    ${PROJECT_DIR}/neo/ui/UserInterface.cpp
    ${PROJECT_DIR}/neo/ui/Window.cpp
    ${PROJECT_DIR}/neo/ui/Winvar.cpp
	)

###############################################################################
# project includes
###############################################################################
set(PROJECT_INCLUDES
	${PROJECT_DIR}/dxsdk_june2010/include
	${PROJECT_DIR}/neo
	)

###############################################################################
# project codes
###############################################################################
set(PROJECT_SRCS 
	${SRCS_CODE}
    )

###############################################################################
# set include dirs for project
###############################################################################
include_directories(
	${PROJECT_INCLUDES}
	)

###############################################################################
# set link dirs for project
###############################################################################
link_directories(
	${PROJECT_OUT_LIB}
	${DX_LIB_DIR}
	)

###############################################################################
# build project.
###############################################################################
add_executable(cDOOM WIN32 ${PROJECT_SRCS})
if(MSVC)
	add_definitions( -D_CRT_SECURE_NO_DEPRECATE -D_CRT_NONSTDC_NO_DEPRECATE )
	set(CMAKE_C_FLAGS_DEBUG   "${CMAKE_C_FLAGS_DEBUG} -DDEBUG -D_DEBUG")
	set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DDEBUG -D_DEBUG")
	target_compile_options(cDOOM PRIVATE /MP /W4 /EHsc)
	target_link_libraries(cDOOM PRIVATE doomclassic xinput dbghelp dinput8 dsound dxguid DxErr glu32 iphlpapi odbc32 odbccp32 opengl32 winmm wsock32 x3daudio)
else()
	target_link_libraries(cDOOM PRIVATE -llibuv -lpthread -luuid )
endif()
 
