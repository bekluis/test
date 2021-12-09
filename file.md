#file

package com.javassem.controller;

import java.util.Date;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

import com.javassem.domain.BoardVO;
import com.javassem.service.BoardService;

@Controller
public class BoardController {

	@Autowired
	private BoardService boardService;

	@RequestMapping("insertBoard.do")
	public void test() {

	}

//	@RequestMapping("saveBoard.do")
//	public String save(BoardVO vo) {
//		boardService.insertBoard(vo);
//		return "home";
//	}

	@RequestMapping("saveBoard.do")
	public String xxxx(BoardVO vo,Model u) {
		//ModelAndView mv = new ModelAndView();
		//mv.setViewName(viewName);
		//mv.addObject("serverTime", new Date());
		u.addAttribute("serverTime", new Date());
		return "home";
	}


	//목록보기
	@RequestMapping("getBoardList.do")
	public void select(String searchCondition, String searchKeyword, Model m) {
		//Map이 부모이고 HashMap이 자식
		Map map = new HashMap();
		map.put("searchCondition",searchCondition);
		map.put("searchKeyword", searchKeyword);


		//map을 집이라 생각
		//BoardVO가 리스트형식이니 List<> 변수명
		List<BoardVO> list = boardService.getBoardList(map);
		m.addAttribute("boardList", list);
	}

	// 해당 글보기
	@RequestMapping("getBoard.do")
	public void getBoard(BoardVO vo,Model m) {
		BoardVO result = boardService.getBoard(vo);
		m.addAttribute("board", result);
		//jsp뷰파일에서 이름 꼭 맞추기
	}

	//	 삭제하기
	@RequestMapping("deleteBoard.do")
	public String delectBoard(BoardVO vo) {
		boardService.deleteBoard(vo);
		return "redirect:getBoardList.do";
	}

	// 수정하기(부분) Model 사용 X
	@RequestMapping("updateBoard.do")
	public String updateBoard(BoardVO vo) {
		boardService.updateBoard(vo);
		return "redirect:getBoard.do?seq=" + vo.getSeq();
	}



	//Model을 사용하였을 때
//	@RequestMapping("updateBoard.do")
//	public String updateBoard(BoardVO vo, Model m) {
//		m.addAttribute("seq",vo.getSeq());
//		return "redirect:getBoard.do";
//
//	}
}
