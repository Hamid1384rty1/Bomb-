# auto_chat_reply.py
# BombSquad 1.7.x Compatible Plugin
# Put this file in:
# Android/data/net.froemling.bombsquad/files/mods/

from __future__ import annotations
import babase
import bascenev1 as bs

class AutoChatPlugin(babase.Plugin):
    """Plugin to auto-reply in chat: cu -> h, fr -> u"""

    def on_app_running(self) -> None:
        # نمایش پیام هنگام لود شدن مود
        babase.screenmessage("Auto Chat Reply Mod Loaded ✅")

        # هوک کردن تابع اصلی chatmessage
        original_chat = bs.chatmessage

        def chat_interceptor(msg: str, clients: list[int] | None = None):
            """Intercept chat messages and auto-reply."""
            text = msg.strip().lower()

            if text == "cu":
                original_chat("h")
            elif text == "fr":
                original_chat("u")

            # پیام اصلی را هم ارسال کن
            original_chat(msg, clients)

        # جایگزین کردن تابع chatmessage با هوک ما
        bs.chatmessage = chat_interceptor
