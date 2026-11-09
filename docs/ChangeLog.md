# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Fixed

- **AICard_英语单词**: 修复点击朗读无声音的问题。原 TTS 接口 `https://tts.wangwangit.com/v1/audio/speech` 已失效（直接请求返回 `403 Forbidden`，带站点 Referer 返回 `500`），导致 `fetch` 抛错后静默失败。现统一改用 `https://tts.sdgarden.top/v1/audio/speech`（实测返回 `200` + `audio/mpeg`，并带 `Access-Control-Allow-Origin: *`，可满足 Anki 预览与 AnkiDroid 的跨域请求）。
- **AICard_英语单词**: 同步更新 `README.md` 中的默认接口说明。

### Changed

- 正面模板、背面模板、README 中的语音合成接口地址由 `tts.wangwangit.com` 替换为 `tts.sdgarden.top`，其余参数（`voice` / `speed` / `pitch` / `style`）保持不变。
